# Vue Lesson 11: Lists and Conditional Content

## What I Learned

This lesson covered Vue's core features for dynamic rendering and user interaction:

- List rendering with `v-for`
- Conditional rendering with `v-if` and `v-show`
- Two-way data binding with `v-model`
- Event handling with `@click`
- Computed properties for dynamic values

## Challenging Points

### 1. Always use `this` to access data/computed properties

In Vue's methods and computed properties, you must use `this` to reference data properties:

```javascript
// Wrong
return taskListIsVisible ? 'Hide List' : 'Show List';

// Correct
return this.taskListIsVisible ? 'Hide List' : 'Show List';
```

Without `this`, JavaScript throws a `ReferenceError` and Vue stops working.

### 2. Mount selector requires `#` for IDs

```javascript
// Wrong
app.mount('assignment');

// Correct
app.mount('#assignment');
```

## Vue Directive Shorthands

Vue provides shorthand syntax for commonly used directives:

| Shorthand | Full Syntax | Purpose |
|-----------|-------------|---------|
| `@click` | `v-on:click` | Event binding |
| `@input` | `v-on:input` | Input event |
| `@submit` | `v-on:submit` | Form submit event |
| `:key` | `v-bind:key` | Bind key attribute |
| `:class` | `v-bind:class` | Bind class attribute |
| `:href` | `v-bind:href` | Bind href attribute |

**Rule**: `@` = `v-on:` and `:` = `v-bind:`

## Conditional Rendering: `v-if` vs `v-show`

Both control element visibility, but work differently:

| Feature | `v-if` | `v-show` |
|---------|--------|----------|
| **How it works** | Adds/removes element from DOM | Toggles CSS `display` property |
| **Performance** | Higher toggle cost | Lower toggle cost |
| **Initial render** | Skips rendering if false | Always renders |
| **Use case** | Infrequently toggled content | Frequently toggled content |

```html
<!-- Removes <ul> from DOM when false -->
<ul v-if="taskListIsVisible">
  <li>Task 1</li>
</ul>

<!-- Sets display:none when false -->
<ul v-show="taskListIsVisible">
  <li>Task 1</li>
</ul>
```

## List Rendering: `v-for`

Iterates over arrays or objects to render elements:

```html
<li v-for="task in tasks" :key="task">{{ task }}</li>
```

**Key points**:
- Always use `:key` for proper list tracking
- Syntax: `item in items` or `(item, index) in items`
- Works with arrays, objects, ranges

```html
<!-- With index -->
<li v-for="(task, index) in tasks" :key="index">
  {{ index }}: {{ task }}
</li>

<!-- With range -->
<li v-for="n in 10" :key="n">{{ n }}</li>
```

## Summary Table

| Directive | Purpose | Example |
|-----------|---------|---------|
| `v-model` | Two-way data binding | `<input v-model="enteredValue">` |
| `v-for` | List rendering | `<li v-for="item in items" :key="item">` |
| `v-if` | Conditional rendering (DOM) | `<div v-if="isVisible">` |
| `v-show` | Conditional display (CSS) | `<div v-show="isVisible">` |
| `@click` | Click event handler | `<button @click="addTask">` |
| `:key` | Unique identifier for v-for | `:key="task.id"` |
