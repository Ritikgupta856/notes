# Zustand — Interview Preparation Guide

> **Real-world context:** The **Synapse AI** project uses **Zustand v5** for global client state (auth session, UI preferences, chat/conversation state, feature flags). This guide is aligned with **v5** APIs (`create`, `useStore`, middleware patterns).

---

## Table of Contents

1. [What is Zustand?](#what-is-zustand)
2. [Why was Zustand created?](#why-was-zustand-created)
3. [Problems with React Context API](#problems-with-react-context-api)
4. [Problems with Redux](#problems-with-redux)
5. [Zustand vs Redux](#zustand-vs-redux)
6. [Zustand vs Context API](#zustand-vs-context-api)
7. [Zustand vs Recoil](#zustand-vs-recoil)
8. [Zustand vs Jotai](#zustand-vs-jotai)
9. [Zustand vs MobX](#zustand-vs-mobx)
10. [Zustand Architecture](#zustand-architecture)
11. [Internal Working](#internal-working)
12. [Store Creation](#store-creation)
13. [Selectors](#selectors)
14. [Shallow Comparison](#shallow-comparison)
15. [Middleware](#middleware)
16. [Persist Middleware](#persist-middleware)
17. [DevTools Middleware](#devtools-middleware)
18. [Subscribe API](#subscribe-api)
19. [Async Actions](#async-actions)
20. [Derived State](#derived-state)
21. [State Updates](#state-updates)
22. [Performance Optimization](#performance-optimization)
23. [Preventing Re-renders](#preventing-re-renders)
24. [Best Practices](#best-practices)
25. [Folder Structure](#folder-structure)
26. [Common Mistakes](#common-mistakes)
27. [Debugging](#debugging)
28. [Production Usage](#production-usage)
29. [Scenario-Based Questions](#scenario-based-questions)
30. [FAANG Questions](#faang-questions)
31. [Senior-Level Questions](#senior-level-questions)
32. [Quick Revision](#quick-revision)
33. [Cheat Sheet](#cheat-sheet)

---

## What is Zustand?

### Q: What is Zustand?

**A:** Zustand (German for "state") is a **small, unopinionated state management library** for React (and vanilla JS). It provides a global store via a hook-based API with minimal boilerplate.

| Property | Detail |
|----------|--------|
| Bundle size | ~1–3 KB (gzipped) |
| API surface | `create`, `set`, `get`, `subscribe` |
| Paradigm | Flux-like (actions update state) but not Redux |
| React integration | Hooks; components re-render only when selected state changes |

```typescript
import { create } from 'zustand';

interface CounterState {
  count: number;
  increment: () => void;
  decrement: () => void;
}

export const useCounterStore = create<CounterState>((set) => ({
  count: 0,
  increment: () => set((state) => ({ count: state.count + 1 })),
  decrement: () => set((state) => ({ count: state.count - 1 })),
}));

// In a component
function Counter() {
  const count = useCounterStore((s) => s.count);
  const increment = useCounterStore((s) => s.increment);
  return <button onClick={increment}>{count}</button>;
}
```

### Q: Is Zustand a replacement for Redux?

**A:** Not always. Zustand replaces Redux when you want **simplicity and speed of development**. Redux remains stronger for **large teams, strict conventions, time-travel debugging at scale, and ecosystem middleware** (sagas, RTK Query at enterprise scale).

### Q: Does Zustand require a Provider?

**A:** **No.** Unlike Context/Redux, Zustand stores work **without wrapping the app in a Provider**. The store is a module-level singleton (by default).

---

## Why was Zustand created?

### Q: Why was Zustand created?

**A:** Zustand was created by **pmndrs** (same team behind React Three Fiber) to solve recurring pain points:

1. **Redux boilerplate** — actions, reducers, dispatch, providers felt heavy for medium apps.
2. **Context re-render issues** — splitting context still caused unnecessary updates.
3. **Over-engineering** — many apps don't need full Flux architecture.
4. **Hook-first DX** — developers wanted `useStore(selector)` ergonomics.
5. **Performance by default** — selector-based subscriptions without manual `memo` everywhere.

**Design goals:**
- Minimal API (`create` + selector)
- No Provider tree
- Works outside React (vanilla `createStore`)
- Composable middleware (persist, devtools, immer)
- TypeScript-first

---

## Problems with React Context API

### Q: What are the main problems with React Context for global state?

**A:**

| Problem | Explanation |
|---------|-------------|
| **Re-renders all consumers** | Any context value change re-renders every component that `useContext`s it, even if they only need one field |
| **No built-in selectors** | You must manually split contexts or memoize value objects |
| **Provider nesting** | Multiple domains → deep provider trees |
| **No middleware** | No persist, devtools, or logging out of the box |
| **Async/side effects** | Context doesn't define how to handle them |
| **Testing** | Must wrap components in providers in every test |

```tsx
// ❌ Problem: changing `theme` re-renders consumers of `user` too
const AppContext = createContext({ user: null, theme: 'light' });

function AppProvider({ children }) {
  const [user, setUser] = useState(null);
  const [theme, setTheme] = useState('light');
  // New object reference every render unless memoized
  return (
    <AppContext.Provider value={{ user, setUser, theme, setTheme }}>
      {children}
    </AppContext.Provider>
  );
}
```

```tsx
// Mitigation: split contexts (still verbose)
<UserContext.Provider>
  <ThemeContext.Provider>
    {children}
  </ThemeContext.Provider>
</UserContext.Provider>
```

**Interview one-liner:** *Context is for dependency injection, not high-frequency global state.*

---

## Problems with Redux

### Q: What problems does Redux have that Zustand avoids?

**A:**

| Redux Pain Point | Zustand Alternative |
|------------------|---------------------|
| Actions + reducers + dispatch ceremony | `set()` directly in store |
| `connect` / `useSelector` + `useDispatch` | Single `useStore` hook |
| Provider required | No Provider |
| Immutable updates verbose | `set({ ... })` or Immer middleware |
| Large bundle (RTK ~10KB+) | ~1–3 KB core |
| Learning curve (middleware, thunks, sagas) | Learn in an afternoon |
| Overkill for UI toggles, modals, prefs | Perfect fit |

```typescript
// Redux (RTK) — more files and concepts
const counterSlice = createSlice({
  name: 'counter',
  initialState: { value: 0 },
  reducers: {
    increment: (state) => { state.value += 1; },
  },
});
// + store config, Provider, typed hooks...

// Zustand — same feature, one file
const useCounterStore = create((set) => ({
  value: 0,
  increment: () => set((s) => ({ value: s.value + 1 })),
}));
```

**When Redux still wins:** huge teams, strict action logs, Redux DevTools time-travel at org scale, RTK Query as single data layer, existing Redux codebase.

---

## Zustand vs Redux

### Q: Compare Zustand and Redux.

**A:**

| Criteria | Zustand | Redux (RTK) |
|----------|---------|-------------|
| Boilerplate | Minimal | Moderate–High |
| Provider | Not required | Required |
| DevTools | Via middleware | First-class |
| Middleware | Composable, optional | Core pattern |
| Learning curve | Low | Medium–High |
| Bundle size | Tiny | Larger |
| Predictability | Good (if disciplined) | Excellent (enforced) |
| SSR | Supported with care | Well-documented patterns |
| Team scale | Startups → mid-size | Enterprise, large teams |

```typescript
// Zustand async — no thunk middleware needed
const useUserStore = create((set) => ({
  user: null,
  loading: false,
  fetchUser: async (id: string) => {
    set({ loading: true });
    const user = await api.getUser(id);
    set({ user, loading: false });
  },
}));
```

**Interview answer:** *"I'd pick Zustand for client UI state and local domain state in apps like Synapse AI. I'd pick Redux when the org already standardizes on it, or when we need RTK Query + strict action auditing across many squads."*

---

## Zustand vs Context API

### Q: When should you use Zustand over Context?

**A:** Use Zustand when:
- State updates frequently (cart, chat, real-time UI)
- Many components need different slices of the same store
- You want persist/devtools without custom wiring
- You want to read/write store **outside React** (router guards, WebSocket handlers)

Use Context when:
- Theme, locale, auth **rarely** changes
- You want zero dependencies
- State is scoped to a subtree (wizard step, form branch)

```typescript
// Zustand: only re-renders when `items.length` changes
const itemCount = useCartStore((s) => s.items.length);

// Context: any cart change re-renders all consumers
const { items } = useContext(CartContext);
```

---

## Zustand vs Recoil

### Q: How does Zustand compare to Recoil?

**A:**

| | Zustand | Recoil |
|---|---------|--------|
| Model | Single store (or multiple stores) | Atoms + selectors graph |
| Maintainer | pmndrs (active) | Meta (development slowed) |
| Provider | None | `<RecoilRoot>` required |
| Async | Manual in actions | `selector` async support |
| Learning curve | Low | Medium (atom families, etc.) |
| Bundle | Smaller | Larger |

**Interview tip:** Recoil's atom graph is powerful for **derived async graphs**; Zustand is simpler for **imperative app state**. Many teams migrated from Recoil to Zustand or Jotai after Recoil's reduced momentum.

---

## Zustand vs Jotai

### Q: Zustand vs Jotai — which to choose?

**A:** Both are from **pmndrs**. Different mental models:

| | Zustand | Jotai |
|---|---------|-------|
| Model | Top-down store | Bottom-up atoms |
| Best for | App-wide state, actions | Fine-grained derived state |
| DevTools | `devtools` middleware | Jotai DevTools |
| Colocation | Store files | Atoms near components |

```typescript
// Jotai style (for contrast)
import { atom, useAtom } from 'jotai';
const countAtom = atom(0);

// Zustand style
const useStore = create((set) => ({ count: 0, inc: () => set((s) => ({ count: s.count + 1 })) }));
```

**Rule of thumb:** Zustand = "one brain for the app." Jotai = "many small pieces of state that compose."

---

## Zustand vs MobX

### Q: How is Zustand different from MobX?

**A:**

| | Zustand | MobX |
|---|---------|------|
| Paradigm | Explicit `set()` | Observable + automatic tracking |
| Mutability | Immutable updates (convention) | Mutable observables |
| Magic | None — you see every update | Proxy-based reactivity |
| React integration | Hooks | `observer()` HOC/wrapper |
| Bundle | Smaller | Larger |
| Debugging | Straightforward | Can be harder (implicit deps) |

```typescript
// MobX — mutable, auto-tracked
class CounterStore {
  count = 0;
  constructor() { makeAutoObservable(this); }
  increment() { this.count++; }
}

// Zustand — explicit updates
const useCounterStore = create((set) => ({
  count: 0,
  increment: () => set((s) => ({ count: s.count + 1 })),
}));
```

**Interview line:** *MobX optimizes for OOP mutable stores; Zustand optimizes for functional, explicit updates and minimal API.*

---

## Zustand Architecture

### Q: Describe Zustand's architecture.

**A:**

```
┌─────────────────────────────────────────────────────┐
│                    React Components                  │
│   useStore(selector)  →  subscribe  →  re-render    │
└──────────────────────────┬──────────────────────────┘
                           │
┌──────────────────────────▼──────────────────────────┐
│              Zustand Store (vanilla)                 │
│  ┌─────────┐  ┌─────────┐  ┌─────────────────────┐  │
│  │  state  │  │ set()   │  │ get()               │  │
│  └─────────┘  └─────────┘  └─────────────────────┘  │
│  ┌──────────────────────────────────────────────┐   │
│  │ Middleware chain (devtools → persist → immer) │   │
│  └──────────────────────────────────────────────┘   │
└──────────────────────────┬──────────────────────────┘
                           │
              subscribe(listener) — non-React consumers
```

**Layers:**
1. **Vanilla store** — `createStore` holds state, listeners, `setState`, `getState`, `subscribe`
2. **React binding** — `create` wraps vanilla store with `useSyncExternalStore` (v5)
3. **Middleware** — wraps `set`, `get`, `store` for cross-cutting concerns
4. **Multiple stores** — one store per domain (auth, ui, chat) is common

### Q: Single store vs multiple stores?

**A:** **Multiple smaller stores** (Synapse AI pattern):
- `useAuthStore` — session, tokens
- `useChatStore` — messages, active thread
- `useUIStore` — sidebar, modals, theme

Benefits: clearer boundaries, smaller selectors, easier code-splitting, less merge conflict surface.

---

## Internal Working

### Q: How does Zustand work internally?

**A (simplified):**

1. **`create(initializer)`** builds a vanilla store with `getState`, `setState`, `subscribe`.
2. **Initializer** receives `(set, get, api)` and returns the initial state object (state + actions).
3. **`set(partial)`** merges partial state (or accepts updater function), notifies listeners.
4. **`useStore(store, selector)`** uses React 18's **`useSyncExternalStore`** to subscribe to the store.
5. On state change, each hook instance runs its **selector**; if result changed (`Object.is`), component re-renders.

```typescript
// Conceptual internals (not actual source)
function createStore(createState) {
  let state;
  const listeners = new Set();

  const setState = (partial) => {
    const next = typeof partial === 'function' ? partial(state) : partial;
    if (!Object.is(next, state)) {
      state = { ...state, ...next };
      listeners.forEach((l) => l());
    }
  };

  const getState = () => state;
  const subscribe = (listener) => {
    listeners.add(listener);
    return () => listeners.delete(listener);
  };

  state = createState(setState, getState, { setState, getState, subscribe });
  return { getState, setState, subscribe };
}
```

### Q: Why `useSyncExternalStore`?

**A:** Ensures **concurrent-safe** reads of external stores in React 18+. Avoids tearing and aligns Zustand with React's subscription model.

### Q: What is `create` vs `createStore`?

**A:**
- **`create`** — returns a React hook (`useBearStore`)
- **`createStore`** — vanilla store, no React; use in workers, tests, or `store.getState()` outside components

```typescript
import { createStore } from 'zustand/vanilla';

const store = createStore(() => ({ count: 0 }));
store.subscribe((state) => console.log(state.count));
```

---

## Store Creation

### Q: How do you create a store in Zustand v5?

**A:**

```typescript
import { create } from 'zustand';

// 1. Basic store
export const useBearStore = create((set) => ({
  bears: 0,
  increase: () => set((state) => ({ bears: state.bears + 1 })),
}));

// 2. TypeScript — separate interface
interface BearState {
  bears: number;
  increase: () => void;
}

export const useBearStore = create<BearState>()((set) => ({
  bears: 0,
  increase: () => set((s) => ({ bears: s.bears + 1 })),
}));

// 3. With initial props (factory pattern)
export const createChatStore = (conversationId: string) =>
  create<ChatState>()((set, get) => ({
    conversationId,
    messages: [],
    send: async (text: string) => {
      const { messages } = get();
      set({ messages: [...messages, { text, id: crypto.randomUUID() }] });
    },
  }));
```

### Q: What are `set`, `get`, and `api`?

**A:**

| API | Purpose |
|-----|---------|
| `set` | Update state; supports partial object or updater `(state) => partial` |
| `get` | Read current state inside actions (avoid stale closures) |
| `api` | `setState`, `getState`, `subscribe` — advanced use |

```typescript
const useStore = create((set, get) => ({
  items: [] as Item[],
  addItem: (item: Item) => {
    set({ items: [...get().items, item] });
  },
  removeById: (id: string) => {
    set({ items: get().items.filter((i) => i.id !== id) });
  },
}));
```

### Q: Slices pattern?

**A:** Compose independent slices into one store (Redux-style modularization without reducers).

```typescript
import { create, StateCreator } from 'zustand';

type AuthSlice = { user: User | null; login: (u: User) => void };
type UISlice = { sidebarOpen: boolean; toggleSidebar: () => void };

const createAuthSlice: StateCreator<AuthSlice & UISlice, [], [], AuthSlice> = (set) => ({
  user: null,
  login: (user) => set({ user }),
});

const createUISlice: StateCreator<AuthSlice & UISlice, [], [], UISlice> = (set) => ({
  sidebarOpen: true,
  toggleSidebar: () => set((s) => ({ sidebarOpen: !s.sidebarOpen })),
});

export const useAppStore = create<AuthSlice & UISlice>()((...args) => ({
  ...createAuthSlice(...args),
  ...createUISlice(...args),
}));
```

---

## Selectors

### Q: What are selectors in Zustand?

**A:** A **selector** is a function `(state) => slice` passed to the store hook. The component re-renders **only when the selected value changes** (reference or primitive equality via `Object.is`).

```typescript
// ✅ Good — subscribe only to `user.name`
const userName = useAuthStore((s) => s.user?.name);

// ❌ Bad — subscribes to entire store; any change re-renders
const store = useAuthStore();
```

### Q: Can selectors return objects?

**A:** Yes, but a **new object every time** causes re-renders unless you use **`shallow`** or return stable references.

```typescript
import { useShallow } from 'zustand/react/shallow';

// v5 recommended: useShallow hook
const { user, login } = useAuthStore(
  useShallow((s) => ({ user: s.user, login: s.login }))
);

// Or select primitives separately
const user = useAuthStore((s) => s.user);
const login = useAuthStore((s) => s.login);
```

### Q: Custom equality function?

**A:**

```typescript
const count = useStore(
  (s) => s.items.length,
  (a, b) => a === b // default is Object.is
);
```

---

## Shallow Comparison

### Q: What is shallow comparison in Zustand?

**A:** **`shallow`** compares first-level keys of two objects/arrays with `Object.is`. Used when a selector returns an object/array and you want re-render only if those top-level references change.

```typescript
import { shallow } from 'zustand/shallow';
import { useShallow } from 'zustand/react/shallow';

// Option 1: useShallow (v5 idiomatic)
const [bears, fish] = useStore(useShallow((s) => [s.bears, s.fish]));

// Option 2: shallow as equality fn (vanilla useStore API)
const { bears, fish } = useStore(
  (s) => ({ bears: s.bears, fish: s.fish }),
  shallow
);
```

### Q: When does shallow NOT help?

**A:** When nested objects mutate internally but top-level reference stays same — always treat state as **immutable**.

```typescript
// ❌ Mutating nested object — shallow won't detect deep change
set((s) => {
  s.user.name = 'Alice'; // if using Immer ok; plain Zustand bad
  return s;
});
```

---

## Middleware

### Q: What is middleware in Zustand?

**A:** Middleware **wraps** the store creator to extend `set`, `get`, or `store`. Applied right-to-left (innermost first).

```typescript
import { create } from 'zustand';
import { devtools } from 'zustand/middleware';
import { persist } from 'zustand/middleware';
import { immer } from 'zustand/middleware/immer';

const useStore = create<State>()(
  devtools(
    persist(
      immer((set) => ({
        count: 0,
        increment: () =>
          set((state) => {
            state.count += 1; // Immer allows "mutation"
          }),
      })),
      { name: 'counter-storage' }
    ),
    { name: 'CounterStore' }
  )
);
```

### Q: Common middleware?

| Middleware | Package | Purpose |
|------------|---------|---------|
| `persist` | `zustand/middleware` | localStorage/sessionStorage sync |
| `devtools` | `zustand/middleware` | Redux DevTools extension |
| `immer` | `zustand/middleware/immer` | Mutable-style updates |
| `subscribeWithSelector` | `zustand/middleware` | Granular `subscribe` |
| `redux` | `zustand/middleware` | Redux reducer compatibility |

### Q: TypeScript + middleware typing?

**A:** Use **double invoke** `create<T>()(...)` so TypeScript infers middleware mutators:

```typescript
import { create } from 'zustand';
import { persist } from 'zustand/middleware';

interface State { bears: number; }

export const useStore = create<State>()(
  persist(
    (set) => ({ bears: 0 }),
    { name: 'bear-storage' }
  )
);
```

---

## Persist Middleware

### Q: How does `persist` work?

**A:** Saves slice of state to **storage** (default `localStorage`), rehydrates on load, supports partial persist, versioning, and migrations.

```typescript
import { create } from 'zustand';
import { persist, createJSONStorage } from 'zustand/middleware';

interface SettingsState {
  theme: 'light' | 'dark';
  setTheme: (theme: 'light' | 'dark') => void;
}

export const useSettingsStore = create<SettingsState>()(
  persist(
    (set) => ({
      theme: 'light',
      setTheme: (theme) => set({ theme }),
    }),
    {
      name: 'synapse-settings', // storage key
      partialize: (state) => ({ theme: state.theme }), // only persist theme
      storage: createJSONStorage(() => localStorage),
      version: 1,
      migrate: (persisted: unknown, version) => {
        // handle schema changes between app versions
        return persisted as SettingsState;
      },
      onRehydrateStorage: () => (state, error) => {
        if (error) console.error('Rehydration failed', error);
        else console.log('Rehydrated', state);
      },
    }
  )
);
```

### Q: SSR + persist pitfalls?

**A:**
- **Hydration mismatch** — server renders default state; client rehydrates from storage → flash or mismatch.
- **Fix:** render persisted UI after `onFinishHydration` or use `skipHydration` + manual `rehydrate()`.

```typescript
const useStore = create(
  persist(
    (set) => ({ ... }),
    { name: 'app', skipHydration: true }
  )
);

// In client-only effect
useEffect(() => {
  useStore.persist.rehydrate();
}, []);
```

### Q: Synapse AI example?

**A:** Persist **UI preferences** (sidebar collapsed, theme) and **draft message** — not tokens or sensitive PII. Use `partialize` to whitelist safe fields only.

---

## DevTools Middleware

### Q: How do you use Redux DevTools with Zustand?

**A:**

```typescript
import { create } from 'zustand';
import { devtools } from 'zustand/middleware';

interface ChatState {
  messages: Message[];
  addMessage: (m: Message) => void;
}

export const useChatStore = create<ChatState>()(
  devtools(
    (set) => ({
      messages: [],
      addMessage: (m) =>
        set(
          (s) => ({ messages: [...s.messages, m] }),
          false,
          'chat/addMessage' // action name in DevTools
        ),
    }),
    { name: 'SynapseChatStore', enabled: process.env.NODE_ENV === 'development' }
  )
);
```

### Q: `set` third argument?

**A:** `set(partial, replace?, actionName?)` — **`actionName`** appears in DevTools for debugging (third param when not replacing).

### Q: Multiple stores in DevTools?

**A:** Give each store a unique `name` in `devtools({ name: '...' })`.

---

## Subscribe API

### Q: How do you subscribe outside React?

**A:**

```typescript
// Subscribe to all changes
const unsub = useBearStore.subscribe((state) => {
  console.log('bears:', state.bears);
});

// Subscribe with selector (needs subscribeWithSelector middleware)
import { subscribeWithSelector } from 'zustand/middleware';

const useStore = create(
  subscribeWithSelector((set) => ({
    count: 0,
    name: 'app',
  }))
);

const unsub = useStore.subscribe(
  (s) => s.count,
  (count, prevCount) => {
    if (count !== prevCount) analytics.track('count_changed', { count });
  }
);

// Cleanup
unsub();
```

### Q: Use cases for `subscribe`?

**A:**
- Analytics when specific field changes
- Syncing to `sessionStorage` without full persist
- WebSocket handlers updating store from outside React
- Unit tests asserting state transitions

```typescript
// Read without subscribing
const token = useAuthStore.getState().token;

// Imperative update outside component
useAuthStore.setState({ token: null });

// Listen once
const unsub = useAuthStore.subscribe((s) => {
  if (s.user) {
    initUserSocket(s.user.id);
    unsub();
  }
});
```

---

## Async Actions

### Q: How do you handle async operations in Zustand?

**A:** Write async functions **inside the store** — no thunk middleware required.

```typescript
interface UserState {
  user: User | null;
  status: 'idle' | 'loading' | 'error' | 'success';
  error: string | null;
  fetchUser: (id: string) => Promise<void>;
  reset: () => void;
}

export const useUserStore = create<UserState>((set, get) => ({
  user: null,
  status: 'idle',
  error: null,

  fetchUser: async (id) => {
    set({ status: 'loading', error: null });
    try {
      const user = await api.users.get(id);
      set({ user, status: 'success' });
    } catch (e) {
      set({ status: 'error', error: (e as Error).message });
    }
  },

  reset: () => set({ user: null, status: 'idle', error: null }),
}));
```

### Q: Race conditions in async?

**A:** Track request id or abort controller:

```typescript
fetchMessages: async (threadId: string) => {
  const requestId = crypto.randomUUID();
  set({ loading: true, activeRequestId: requestId });

  const messages = await api.getMessages(threadId);

  // Ignore stale response
  if (get().activeRequestId !== requestId) return;
  set({ messages, loading: false });
},
```

### Q: Should async live in Zustand or React Query?

**A:** **Server state** → TanStack Query (cache, stale time, deduping). **Client state** (UI, selections, optimistic UI overlay) → Zustand. Synapse AI pattern: React Query for API data; Zustand for active conversation UI + ephemeral state.

---

## Derived State

### Q: How do you implement derived state?

**A:** Three approaches:

**1. Compute in selector (preferred — no duplication)**

```typescript
const completedCount = useTodoStore(
  (s) => s.todos.filter((t) => t.done).length
);
```

**2. Getter in store**

```typescript
const useStore = create((get) => ({
  items: [] as Item[],
  get total() {
    return get().items.reduce((sum, i) => sum + i.price, 0);
  },
}));
// Note: getters don't work well as stable selectors — prefer selector fn
```

**3. Derive in component with `useMemo`**

```typescript
const todos = useTodoStore((s) => s.todos);
const active = useMemo(() => todos.filter((t) => !t.done), [todos]);
```

### Q: Store derived values that update with state?

**A:**

```typescript
const useStore = create((set, get) => ({
  items: [] as { price: number }[],
  addItem: (item) => set({ items: [...get().items, item] }),
  // Function — always fresh when called
  getTotal: () => get().items.reduce((s, i) => s + i.price, 0),
}));

// In component
const getTotal = useStore((s) => s.getTotal);
const total = getTotal();
```

---

## State Updates

### Q: How does `set` work?

**A:**

```typescript
// Partial merge (default)
set({ count: 1 });

// Functional update
set((state) => ({ count: state.count + 1 }));

// Replace entire state (rare)
set({ count: 0 }, true); // second arg replace = true
```

### Q: Immutable update patterns?

**A:**

```typescript
// Array add
set((s) => ({ todos: [...s.todos, newTodo] }));

// Array remove
set((s) => ({ todos: s.todos.filter((t) => t.id !== id) }));

// Nested update
set((s) => ({
  user: s.user ? { ...s.user, name: 'Alice' } : null,
}));

// With Immer middleware
set((s) => {
  s.user!.name = 'Alice';
});
```

### Q: Batching updates?

**A:** Multiple `set` calls in same synchronous tick → one notification batch (listeners run per set in microtask; React 18 batches re-renders). For multiple updates, prefer single `set`:

```typescript
// ✅ One notification
set({ loading: false, data, error: null });

// ⚠️ Multiple sets work but less clean
set({ loading: false });
set({ data });
```

---

## Performance Optimization

### Q: How do you optimize Zustand performance?

**A:**

1. **Narrow selectors** — select primitives or stable refs
2. **`useShallow`** for multi-field object selections
3. **Split stores** by update frequency
4. **Don't put huge lists in one store** without virtualization
5. **`partialize` in persist** — avoid serializing megabytes
6. **Memoize expensive selectors** outside store if needed
7. **Actions on store** — don't recreate inline in components

```typescript
// ✅ Stable action reference — safe to put in deps
const send = useChatStore((s) => s.send);

// Split fast-changing from slow-changing
// useChatStore — messages (high frequency)
// useUIStore — layout (low frequency)
```

### Q: Colocate components with store slices?

**A:** A child that only needs `messageCount` should not import parent that reads full `messages` array.

---

## Preventing Re-renders

### Q: Why is my component re-rendering on every store update?

**A:** Common causes:

| Cause | Fix |
|-------|-----|
| No selector — `useStore()` | Add `(s) => s.field` |
| Selector returns new object/array | `useShallow` or split selectors |
| Selecting entire nested object | Select primitive fields |
| Parent re-renders | `React.memo` on child |
| Inline selector function | Define stable selector outside or use `useCallback` |

```typescript
// ❌ New object every time → always "changed"
const data = useStore((s) => ({ a: s.a, b: s.b }));

// ✅
const data = useStore(useShallow((s) => ({ a: s.a, b: s.b })));
```

### Q: `React.memo` + Zustand?

**A:** Works well — child with narrow selector only re-renders when its slice changes, regardless of parent.

```typescript
const MessageCount = React.memo(function MessageCount() {
  const count = useChatStore((s) => s.messages.length);
  return <span>{count}</span>;
});
```

---

## Best Practices

### Q: Zustand best practices for production?

**A:**

1. **One store per domain** — auth, ui, feature modules
2. **Colocate types** — `interface AuthState` next to store
3. **Actions inside store** — keep components thin
4. **Selectors in components** — or export custom hooks:

```typescript
// hooks/useAuth.ts
export const useUser = () => useAuthStore((s) => s.user);
export const useLogin = () => useAuthStore((s) => s.login);
```

5. **Never store secrets in persist** — tokens in memory or httpOnly cookies
6. **Use TypeScript** `create<State>()(...)` with middleware
7. **Name DevTools actions** for traceability
8. **Test stores in isolation** — no React needed
9. **Server state in React Query**, client state in Zustand
10. **Document rehydration** for SSR apps

### Q: Should everything go in Zustand?

**A:** No. Keep **local `useState`** for form inputs, **URL state** in router, **server cache** in Query/SWR.

---

## Folder Structure

### Q: Recommended folder structure?

**A (Synapse AI–style):**

```
src/
├── stores/
│   ├── auth.store.ts        # useAuthStore
│   ├── chat.store.ts        # useChatStore
│   ├── ui.store.ts          # useUIStore
│   ├── index.ts             # re-exports
│   └── types/
│       ├── auth.types.ts
│       └── chat.types.ts
├── hooks/
│   ├── useAuth.ts           # thin selectors over auth store
│   └── useChat.ts
├── features/
│   └── chat/
│       ├── ChatPanel.tsx
│       └── chat.utils.ts
```

**Alternative (feature-first):**

```
features/chat/store.ts
features/auth/store.ts
shared/stores/ui.store.ts
```

**Interview tip:** Pick **domain stores + feature folders** for mid/large apps; avoid one giant `store.ts`.

---

## Common Mistakes

### Q: What are common Zustand mistakes?

**A:**

| Mistake | Problem | Fix |
|---------|---------|-----|
| `useStore()` without selector | Re-render on any change | Use selector |
| Storing server data long-term | Stale cache | React Query |
| Persisting tokens | XSS risk | Memory / httpOnly cookie |
| Mutating state directly | No re-render / bugs | Immutable `set` or Immer |
| One giant store | Performance + maintenance | Split stores |
| Derived state duplicated | Sync bugs | Derive in selector |
| Creating store in component | New store per render | Module-level `create` |
| Ignoring hydration (SSR) | UI flash | `skipHydration` + manual rehydrate |
| Overusing `shallow` | Hides selector smell | Prefer primitive selectors |

```typescript
// ❌ Store inside component — WRONG
function Bad() {
  const useStore = create(() => ({})); // new store every render!
}

// ✅ Module scope
const useStore = create(() => ({}));
```

---

## Debugging

### Q: How do you debug Zustand stores?

**A:**

1. **Redux DevTools** — `devtools` middleware, named actions
2. **`subscribe` logging** in development:

```typescript
if (process.env.NODE_ENV === 'development') {
  useAuthStore.subscribe((state, prev) => {
    console.log('Auth changed', { prev, next: state });
  });
}
```

3. **React DevTools** — inspect which components re-render
4. **`store.getState()`** in console — `window.useAuthStore = useAuthStore` (dev only)
5. **Why did you render** — `@welldone-software/why-did-you-render`
6. **Check selector** — log selector output in component

```typescript
// Temporary debug middleware
const log = (config) => (set, get, api) =>
  config(
    (...args) => {
      console.log('  applying', args);
      set(...args);
      console.log('  new state', get());
    },
    get,
    api
  );
```

---

## Production Usage

### Q: How is Zustand used in production (e.g., Synapse AI)?

**A:**

**Stack:** Zustand v5 + TypeScript + persist (UI prefs) + devtools (dev only) + TanStack Query (API).

**Typical split:**

| Store | Holds | Persist? |
|-------|-------|----------|
| `useAuthStore` | user profile, auth status | No (or refresh token via secure channel only) |
| `useChatStore` | active thread, draft, optimistic msgs | Draft only (`partialize`) |
| `useUIStore` | sidebar, modals, theme | Yes |

**Checklist:**
- [ ] DevTools disabled in production build
- [ ] `partialize` excludes sensitive fields
- [ ] Migration version in persist for deploys
- [ ] Error boundaries around features, not around store
- [ ] E2E tests seed state via `setState` or API
- [ ] Lazy load feature stores if code-splitting

```typescript
export const useUIStore = create<UIState>()(
  devtools(
    persist(
      (set) => ({
        sidebarCollapsed: false,
        toggleSidebar: () =>
          set((s) => ({ sidebarCollapsed: !s.sidebarCollapsed })),
      }),
      {
        name: 'synapse-ui-v1',
        partialize: (s) => ({ sidebarCollapsed: s.sidebarCollapsed }),
      }
    ),
    { enabled: import.meta.env.DEV }
  )
);
```

---

## Scenario-Based Questions

### Q1: User logs out — what do you reset?

**A:** Clear auth store, invalidate React Query cache, reset chat ephemeral state, optionally clear persist keys:

```typescript
logout: () => {
  useAuthStore.setState({ user: null, token: null });
  useChatStore.setState({ messages: [], activeThreadId: null });
  queryClient.clear();
  useUIStore.persist.clearStorage(); // if needed
},
```

### Q2: Real-time WebSocket messages arrive — where to handle?

**A:** WebSocket module calls `useChatStore.getState().appendMessage(msg)` — no React needed. Components subscribed to `messages` re-render.

### Q3: Form with 20 fields causes lag — Zustand?

**A:** Prefer **local `useState`** or **React Hook Form** for field-level updates. Zustand for submit payload or wizard step index, not every keystroke (unless isolated store + field selectors).

### Q4: Two tabs open — state sync?

**A:** `persist` + `storage` event listener, or `BroadcastChannel`:

```typescript
window.addEventListener('storage', (e) => {
  if (e.key === 'synapse-ui-v1') useUIStore.persist.rehydrate();
});
```

### Q5: Migrate from Context to Zustand?

**A:** Extract one context at a time; replace `useContext` with selector hooks; remove Provider from tree; measure re-renders before/after.

---

## FAANG Questions

### Q: Design a global notification/toast system with Zustand.

**A:**

```typescript
interface Toast { id: string; message: string; type: 'info' | 'error' }
interface ToastState {
  toasts: Toast[];
  add: (message: string, type?: Toast['type']) => void;
  remove: (id: string) => void;
}

export const useToastStore = create<ToastState>((set, get) => ({
  toasts: [],
  add: (message, type = 'info') => {
    const id = crypto.randomUUID();
    set({ toasts: [...get().toasts, { id, message, type }] });
    setTimeout(() => get().remove(id), 5000);
  },
  remove: (id) =>
    set({ toasts: get().toasts.filter((t) => t.id !== id) }),
}));
```

### Q: How would you test a Zustand store?

**A:**

```typescript
import { act } from '@testing-library/react';
import { useCounterStore } from './counter.store';

beforeEach(() => {
  useCounterStore.setState({ count: 0 });
});

it('increments', () => {
  act(() => {
    useCounterStore.getState().increment();
  });
  expect(useCounterStore.getState().count).toBe(1);
});
```

### Q: Explain tearing in concurrent React and how Zustand avoids it.

**A:** Tearing = UI shows mixed state from different renders during concurrent updates. Zustand uses **`useSyncExternalStore`**, which tells React to synchronously read consistent snapshot from external store during render.

### Q: Implement undo/redo.

**A:** Middleware or manual history stack:

```typescript
const useHistoryStore = create((set, get) => ({
  past: [] as State[],
  present: initialState,
  future: [] as State[],
  set: (partial) => {
    const { past, present } = get();
    set({
      past: [...past, present],
      present: { ...present, ...partial },
      future: [],
    });
  },
  undo: () => {
    const { past, present, future } = get();
    if (!past.length) return;
    const previous = past[past.length - 1];
    set({
      past: past.slice(0, -1),
      present: previous,
      future: [present, ...future],
    });
  },
}));
```

### Q: Code review: what's wrong?

```typescript
const useStore = create((set) => ({
  data: expensiveComputation(),
  update: () => set({ data: expensiveComputation() }),
}));
```

**A:** `expensiveComputation()` runs on **every store creation and update** — should run lazily on first access or in selector/`useMemo`. Initial call blocks store init.

---

## Senior-Level Questions

### Q: When would you NOT choose Zustand for a greenfield app?

**A:** When the org mandates Redux, when you need **distributed event sourcing**, when **complex async orchestration** (sagas) is central, or when the team is already expert in MobX/RTK Query-only architecture.

### Q: How do you scale Zustand across 50+ engineers?

**A:** Domain-owned stores, lint rules (no default `useStore()`), shared selector hooks, ADRs for server vs client state, contract tests on store shapes, versioned persist migrations, CODEOWNERS per `stores/`.

### Q: Discuss SSR architecture with Zustand + Next.js App Router.

**A:** Stores are client singletons — use **`'use client'`** boundary. Avoid persist hydration mismatch with `skipHydration`. Don't serialize client store into RSC props; pass server data as props and **hydrate store in `useEffect`** once.

### Q: Security review concerns?

**A:** XSS + `localStorage` persist = token theft. CSP, no secrets in persist, sanitize before render, short-lived tokens, prefer httpOnly cookies for session.

### Q: Performance audit findings — chat app with 10k messages in store.

**A:** Virtualize list; store **message ids** not full objects if Query holds cache; normalize by id; subscribe to `visibleRange` not full array; consider IndexedDB for archive via custom persist storage.

### Q: Design cross-tab auth sync.

**A:** `storage` event on auth key, or `BroadcastChannel` posting logout/login events, calling `setState` on all tabs.

### Q: Compare storing normalized vs denormalized state.

**A:** Normalized (`byId`, `ids`) — O(1) updates, harder selectors. Denormalized — simpler reads, expensive array maps. Chat apps often normalize messages by `id`.

---

## Quick Revision

### 30-Second Pitch
Zustand = minimal global state, hook + selector, no Provider, ~1KB, v5 uses `useSyncExternalStore`, middleware for persist/devtools/immer.

### Remember
- **Selector** = performance
- **`shallow` / `useShallow`** = object selections
- **`get()`** = read in actions
- **`subscribe`** = outside React
- **Server state** → Query; **client state** → Zustand
- **Synapse AI** uses v5, domain stores, selective persist

### v5 API Shifts (from v4)
- Named import: `import { create } from 'zustand'`
- `useShallow` from `zustand/react/shallow`
- `create<T>()(...)` for middleware TS inference

### Decision Tree
```
Need global state?
├─ Rare updates, few consumers → Context OK
├─ Server/API cache → TanStack Query
├─ Fine-grained atoms → Jotai
├─ Enterprise Redux shop → RTK
└─ Default sweet spot → Zustand
```

---

## Cheat Sheet

### Install

```bash
npm install zustand
# optional
npm install immer  # for immer middleware
```

### Create Store

```typescript
import { create } from 'zustand';

export const useStore = create((set, get) => ({
  // state
  count: 0,
  // sync action
  inc: () => set((s) => ({ count: s.count + 1 })),
  // async action
  fetch: async () => {
    const data = await fetch('/api').then((r) => r.json());
    set({ data });
  },
}));
```

### Use in Component

```typescript
const count = useStore((s) => s.count);
const inc = useStore((s) => s.inc);

// multiple fields
import { useShallow } from 'zustand/react/shallow';
const { count, inc } = useStore(useShallow((s) => ({ count: s.count, inc: s.inc })));
```

### Outside React

```typescript
useStore.getState().count;
useStore.setState({ count: 0 });
const unsub = useStore.subscribe(console.log);
```

### Middleware Stack

```typescript
import { create } from 'zustand';
import { devtools, persist } from 'zustand/middleware';
import { immer } from 'zustand/middleware/immer';

const useStore = create()(
  devtools(persist(immer((set) => ({ ... })), { name: 'key' }))
);
```

### Persist Essentials

```typescript
persist(stateCreator, {
  name: 'storage-key',
  partialize: (s) => ({ safe: s.safe }),
  version: 1,
  migrate: (persisted, version) => persisted,
});
```

### DevTools Action Names

```typescript
set({ count: 1 }, false, 'counter/increment');
```

### TypeScript Pattern

```typescript
interface State { foo: string; setFoo: (v: string) => void; }
const useStore = create<State>()((set) => ({
  foo: '',
  setFoo: (foo) => set({ foo }),
}));
```

### Performance Checklist

- [ ] Always use selector
- [ ] `useShallow` for object/array picks
- [ ] Split stores by update rate
- [ ] Don't persist secrets
- [ ] DevTools off in prod

### vs Alternatives (One Line Each)

| Lib | One-liner |
|-----|-----------|
| Redux | Structured, verbose, enterprise |
| Context | DI, not frequent global state |
| Recoil | Atom graph, Meta slowdown |
| Jotai | Atoms, bottom-up |
| MobX | Observable OOP magic |

### Interview One-Liners

1. **No Provider** — module singleton store
2. **Re-renders** — controlled by selector + `Object.is`
3. **Async** — plain async in actions, no thunk
4. **SSR** — client-only; mind persist hydration
5. **Synapse AI** — Zustand v5 for client UI + chat UX; Query for API

---

*Last updated for Zustand v5 — aligned with Synapse AI project patterns.*
