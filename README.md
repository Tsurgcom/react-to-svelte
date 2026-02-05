# React to Svelte 5 Converter Skill

An OpenCode skill for converting React components to Svelte 5 using modern runes syntax.

## Overview

This skill provides comprehensive instructions for migrating React components to Svelte 5, covering:

- **State Management**: `useState` → `$state`, `useReducer` patterns
- **Derived Values**: `useMemo` → `$derived`, `useCallback` simplification
- **Side Effects**: `useEffect` → `$effect`, `useLayoutEffect` → `$effect.pre`
- **Props**: Destructuring → `$props()` with TypeScript support
- **Pure Components**: Automatic purity in Svelte (no memo needed)
- **Event Handling**: React events → Svelte events
- **Rendering**: JSX → Svelte templates with `{#if}` and `{#each}`
- **Context**: `createContext/useContext` → `setContext/getContext`
- **Refs**: `useRef` → `bind:this`
- **Forms**: Two-way binding with `bind:value`
- **Custom Hooks**: Converting to Svelte 5 runes-based functions
- **Accessibility**: ARIA attributes, keyboard events, focus management, reduced motion

## Installation

### Local Project
```bash
mkdir -p .opencode/skills/react-to-svelte
cp SKILL.md .opencode/skills/react-to-svelte/
```

### Global Installation
```bash
mkdir -p ~/.config/opencode/skills/react-to-svelte
cp SKILL.md ~/.config/opencode/skills/react-to-svelte/
```

## Usage

Once installed, OpenCode agents can load this skill automatically or you can invoke it:

```
/skill react-to-svelte
```

Then ask the agent to convert a React component:

```
Convert this React component to Svelte 5:
[paste your React code]
```

## Features

### Comprehensive Pattern Coverage
- All React hooks (useState, useEffect, useMemo, useCallback, useRef, useContext, useReducer)
- Pure components and optimization patterns
- Event handling and custom events
- Conditional and list rendering
- Context API migration
- Form handling with two-way binding
- Component composition (slots vs children)
- Custom hooks to Svelte 5 functions

### Accessibility Focus
- ARIA attribute preservation
- Keyboard event handling
- Focus management patterns
- Screen reader support
- Reduced motion preferences
- Svelte's built-in a11y warnings

### Migration Support
- Step-by-step conversion checklist
- Common pitfalls and solutions
- Before/after code examples
- TypeScript integration

## Examples

### Basic Component

**React:**
```jsx
function Counter({ initial = 0 }) {
  const [count, setCount] = useState(initial);
  return <button onClick={() => setCount(c => c + 1)}>{count}</button>;
}
```

**Svelte 5:**
```svelte
<script>
  let { initial = 0 } = $props();
  let count = $state(initial);
</script>

<button onclick={() => count++}>
  {count}
</button>
```

### Complex Example with Effects

**React:**
```jsx
function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  
  useEffect(() => {
    fetch(`/api/users/${userId}`)
      .then(r => r.json())
      .then(data => {
        setUser(data);
        setLoading(false);
      });
  }, [userId]);
  
  if (loading) return <div>Loading...</div>;
  return <div>{user.name}</div>;
}
```

**Svelte 5:**
```svelte
<script>
  let { userId } = $props();
  let user = $state(null);
  let loading = $state(true);
  
  $effect(() => {
    fetch(`/api/users/${userId}`)
      .then(r => r.json())
      .then(data => {
        user = data;
        loading = false;
      });
  });
</script>

{#if loading}
  <div>Loading...</div>
{:else}
  <div>{user.name}</div>
{/if}
```

## Migration Checklist

- [ ] Rename file from `.jsx/.tsx` to `.svelte`
- [ ] Remove React imports
- [ ] Convert function to Svelte structure
- [ ] Convert `useState` to `$state`
- [ ] Convert `useEffect` to `$effect`
- [ ] Convert `useMemo` to `$derived`
- [ ] Convert props to `$props()`
- [ ] Convert event handlers
- [ ] Convert conditional rendering to `{#if}` blocks
- [ ] Convert `.map()` to `{#each}` blocks
- [ ] Convert `useContext` to `getContext`
- [ ] Convert `useRef` to `bind:this`
- [ ] Add scoped styles
- [ ] Review accessibility attributes
- [ ] Test component behavior

## Compatibility

- **OpenCode**: Native support
- **Svelte Version**: 5.x (runes syntax)
- **TypeScript**: Full support with type examples

## Contributing

Feel free to open issues or PRs to improve this skill.

## License

MIT

## Resources

- [Svelte 5 Documentation](https://svelte.dev/docs)
- [Svelte Runes](https://svelte.dev/docs/runes)
- [OpenCode Skills](https://open-code.ai/en/docs/skills)
