# Unpoly Complete Cheatsheet

---
## up.link (Linking to Fragments)

### HTML Attributes
- `up-target`: Updates only the targeted fragment.
  - Example:
    ```html
    <a href="/users" up-target=".list">Users</a>
    ```
- `up-follow`: Follows link via JS and updates fragment.
  - Example:
    ```html
    <a href="/users" up-follow>Users</a>
    ```
- `up-instant`: Activates link on mousedown instead of click.
  - Example:
    ```html
    <a href="/users" up-instant>Users</a>
    ```
- `up-preload`: Preloads link before click.
  - Example:
    ```html
    <a href="/users" up-preload>Users</a>
    ```
- `up-clickable` *(experimental)*: Enables keyboard interaction for non-interactive elements.
  - Example:
    ```html
    <div up-clickable>Click me</div>
    ```
- `up-expand`: Enlarges the click area of a descendant link.
  - Example:
    ```html
    <div up-expand><a href="/users">Users</a></div>
    ```
- `up-dash` *(deprecated)*: Follows link as fast as possible.
  - Example:
    ```html
    <a href="/users" up-dash>Users</a>
    ```
- `up-href` *(deprecated)*: Makes any element behave like a hyperlink.
  - Example:
    ```html
    <div up-href="/users">Users</div>
    ```
- `up-defer`: Placeholder for content loaded later.
  - Example:
    ```html
    <div up-defer="/more">Loading...</div>
    ```

### JavaScript API
- `up.follow(link, [options])`: Follows the given link and updates a fragment.
  - Example:
    ```js
    up.follow(document.querySelector('a'), {target: '.list'})
    ```
- `up.link.config`: Configures defaults for link handling.
  - Example:
    ```js
    up.link.config.followDelay = 100
    ```
- `up.link.isFollowable(link)`: Returns whether the link will be followed by Unpoly.
  - Example:
    ```js
    up.link.isFollowable(document.querySelector('a'))
    ```
- `up.link.preload(link, [options])`: Preloads a GET link.
  - Example:
    ```js
    up.link.preload(document.querySelector('a'))
    ```
- `up.link.followOptions(link)`: Parses render options for a link.
  - Example:
    ```js
    up.link.followOptions(document.querySelector('a'))
    ```
- `up.link.isSafe(link)`: Returns whether the link uses a safe HTTP method.
  - Example:
    ```js
    up.link.isSafe(document.querySelector('a'))
    ```
- `up.link.makeFollowable(link)` *(experimental)*: Ensures the link is followed by Unpoly.
  - Example:
    ```js
    up.link.makeFollowable(document.querySelector('a'))
    ```

### Events
- `up:link:follow`: Emitted when a link is followed.
  - Example:
    ```js
    document.addEventListener('up:link:follow', fn)
    ```
- `up:link:preload`: Emitted before a link is preloaded.
  - Example:
    ```js
    document.addEventListener('up:link:preload', fn)
    ```
- `up:click`: Click event honoring `up-instant`.
  - Example:
    ```js
    document.addEventListener('up:click', fn)
    ```

---
## up.script (Custom JavaScript)

### HTML Attributes
- `up-data`: Attaches structured data to an element.
  - Example:
    ```html
    <div up-data='{"foo": "bar"}'>Hello</div>
    ```
- `up-asset`: Tracks an element as a frontend asset (JS/CSS).
  - Example:
    ```html
    <script src="app.js" up-asset></script>
    ```

### JavaScript API
- `up.compiler(selector, [options], fn)`: Registers a function for elements inserted into the DOM.
  - Example:
    ```js
    up.compiler('.my-widget', el => { /* ... */ })
    ```
- `up.macro(selector, options, macro)`: Registers a macro compiler run before others.
  - Example:
    ```js
    up.macro('.macro', {}, el => { /* ... */ })
    ```
- `up.hello(element, [options])`: Manually compiles a fragment inserted by external code.
  - Example:
    ```js
    up.hello(document.querySelector('.new-fragment'))
    ```
- `up.data(element)`: Returns the data attached to an element.
  - Example:
    ```js
    up.data(document.querySelector('[up-data]'))
    ```
- `up.destructor(element, fn)`: Registers a function to run when element is destroyed.
  - Example:
    ```js
    up.destructor(el, () => alert('Destroyed'))
    ```
- `up.script.config`: Configures script handling and asset tracking.
  - Example:
    ```js
    up.script.config.assetSelector = 'script, link'
    ```
- `up:assets:changed`: Emitted when frontend code changes while running.
  - Example:
    ```js
    document.addEventListener('up:assets:changed', fn)
    ```
- `up.$compiler` *(deprecated)*: jQuery-based compiler registration.
- `up.$macro` *(deprecated)*: jQuery-based macro registration.

---
## up.form (Forms)

### HTML Attributes
- `up-submit`: Submits form via JS, updates fragment.
  - Example: `<form up-submit>...</form>`
- `up-validate`: Renders new form state on field change.
  - Example: `<input up-validate>`
- `up-switch`: Controls state of another element when field changes.
  - Example: `<select up-switch="#details">...</select>`
- `up-autosubmit`: Auto-submit form on field change.
  - Example: `<form up-autosubmit>...</form>`
- `up-disable-for`: Disables element while a field with `up-switch` has a value.
  - Example: `<button up-disable-for="no">Submit</button>`
- `up-enable-for`: Enables element while a field with `up-switch` has a value.
  - Example: `<button up-enable-for="yes">Submit</button>`
- `up-form-group`: Marks element as a form group.
  - Example: `<div up-form-group>...</div>`
- `up-hide-for`: Hides element while a field with `up-switch` has a value.
  - Example: `<div up-hide-for="no">Hidden</div>`
- `up-show-for`: Shows element if a field with `up-switch` has a value.
  - Example: `<div up-show-for="yes">Shown</div>`
- `up-watch`: Watches form fields and runs callback on change.
  - Example: `<input up-watch>`
- `up-fieldset` *(deprecated)*: Marks element as a form group.
- `up-observe` *(deprecated)*: Watches form fields for changes.

### JavaScript API
- `up.watch(element, [options], callback)`: Watches fields and runs callback on change.
  - Example: `up.watch(form, {}, () => alert('Changed'))`
- `up.submit(form, [options])`: Submits form via AJAX and updates fragment.
  - Example: `up.submit(document.querySelector('form'))`
- `up.validate(element, options)`: Renders new form state from current field values.
  - Example: `up.validate(document.querySelector('input'))`
- `up.autosubmit(element, [options])`: Auto-submit form on field change.
  - Example: `up.autosubmit(document.querySelector('form'))`
- `up.form.config`: Sets default options for form submission/validation.
  - Example: `up.form.config.autosubmitDelay = 300`
- `up.form.fields(root)`: Returns list of form fields within element.
  - Example: `up.form.fields(document.querySelector('form'))`
- `up.form.group(element)` *(experimental)*: Returns form group for element.
- `up.form.isField(element)`: Returns whether element is a form field.
  - Example: `up.form.isField(document.querySelector('input'))`
- `up.form.isSubmittable(form)`: Returns whether form will be submitted via Unpoly.
  - Example: `up.form.isSubmittable(document.querySelector('form'))`
- `up.form.submitButtons(root)` *(experimental)*: Returns list of submit buttons.
- `up.form.submitOptions(form)`: Parses render options for form.
- `up.observe(elements, [options], onChange)` *(deprecated)*: Observes fields for changes.

### Events
- `up:form:submit`: Emitted when form is submitted via Unpoly.
  - Example: `document.addEventListener('up:form:submit', fn)`
- `up:form:validate`: Emitted before form is validated.
  - Example: `document.addEventListener('up:form:validate', fn)`
- `up:form:switch`: Emitted when a field with `up-switch` changes.
  - Example: `document.addEventListener('up:form:switch', fn)`

---
## up.layer (Layers)

### HTML Attributes
- `up-layer="new"`: Shows response in new overlay.
  - Example: `<a href="/dialog" up-layer="new">Open dialog</a>`
- `up-accept`: Accepts current layer when clicked/submitted.
  - Example: `<button up-accept>OK</button>`
- `up-dismiss`: Dismisses current layer when clicked/submitted.
  - Example: `<button up-dismiss>Cancel</button>`
- `up-close` *(deprecated)*: Closes currently open overlay.
- `up-drawer` *(deprecated)*: Opens modal drawer overlay.
- `up-modal` *(deprecated)*: Opens modal overlay.
  - Example: `<a href="/dialog" up-modal>Open modal</a>`
- `up-popup` *(deprecated)*: Opens popup overlay.

### JavaScript API
- `up.layer.current`: Returns current layer in stack.
  - Example: `up.layer.current`
- `up.layer.on(types, [selector], [options], listener)`: Listens to DOM event in current layer.
  - Example: `up.layer.on('click', '.btn', {}, fn)`
- `up.layer.ask(options)`: Opens overlay, returns promise for acceptance.
  - Example: `up.layer.ask({content: 'Are you sure?'})`
- `up.layer.accept([value], [options])`: Accepts current layer.
  - Example: `up.layer.accept('ok')`
- `up.layer.dismiss([value], [options])`: Dismisses current layer.
  - Example: `up.layer.dismiss('cancel')`
- `up.layer.open([options])`: Opens new overlay.
  - Example: `up.layer.open({content: 'Hello'})`
- `up.layer.config`: Configures default attributes for overlays.
- `up.layer.contains(element)`: Returns whether element is in current layer.
- `up.layer.count`: Number of layers in stack.
- `up.layer.front`: Returns frontmost layer.
- `up.layer.get([value])`: Returns up.Layer object for element/layer option.
- `up.layer.getAll([layer])` *(experimental)*: Array of up.Layer objects matching option.
- `up.layer.history`: Whether updates in current layer affect browser history.
- `up.layer.isFront()`: Is current layer frontmost?
- `up.layer.isOverlay()`: Is current layer not root?
- `up.layer.isRoot()`: Is current layer root?
- `up.layer.location`: Location URL of current layer.
- `up.layer.mode`: Current layer's mode.
- `up.layer.off(types, listener)`: Unbinds event listener.
- `up.layer.overlays`: Array of all overlays.
- `up.layer.parent`: Parent layer of current layer.
- `up.layer.root`: Root layer.
- `up.layer.size`: Size of current layer.
- `up.layer.stack`: List of open layers.
- `up.layer.affix(selector, [attrs])` *(experimental)*: Creates element and appends to layer.
- `up.layer.context` *(experimental)*: Context of current layer.
- `up.layer.emit`: Emits event on outmost element.

### Events
- `up:layer:accept`: Before layer is accepted.
- `up:layer:accepted`: After layer accepted.
- `up:layer:dismiss`: Before layer is dismissed.
- `up:layer:dismissed`: After layer dismissed.
- `up:layer:open`: Before overlay is opened.
- `up:layer:opened`: After overlay placed in DOM.
- `up:layer:location:changed`: After layer's location changes.

---
## up.fragment (Fragment API)

### HTML Attributes
- `up-keep`: Persist element when rendering.
  - Example: `<div up-keep>...</div>`
- `up-id`: Sets unique identifier for element.
  - Example: `<div up-id="user-1">...</div>`
- `up-main`: Marks as primary content element.
  - Example: `<main up-main>...</main>`
- `up-source`: Set to URL from which fragment loaded.
  - Example: `<div up-source="/users">...</div>`
- `up-etag`: Sets ETag for fragment's data.
  - Example: `<div up-etag="abc123">...</div>`
- `up-time`: Sets last change time for fragment's data.
  - Example: `<div up-time="2025-07-16T12:00:00Z">...</div>`
- `.up-destroying`: Class for elements being removed by transition.

### CSS Selectors
- `:layer`: Matches layer's topmost swappable element.
- `:main`: Matches layer's main content area.
- `:maybe`: Marks selector as optional.
- `:none`: Server request without changing fragment.
- `:origin`: References origin element that triggered change.

### JavaScript API
- `up.render([target], [options])`: Replaces elements with server response/HTML string.
  - Example: `up.render('.list', {url: '/users'})`
- `up.destroy(element, [options])`: Destroys element/selector.
  - Example: `up.destroy('.old')`
- `up.reload([element], [options])`: Replaces element with fresh copy from server.
  - Example: `up.reload('.list')`
- `up.fragment.get([root], selector, [options])`: Returns first fragment matching selector.
  - Example: `up.fragment.get(document, '.list')`
- `up.fragment.all([root], selector, [options])`: Returns all matching elements, ignoring destroyed.
- `up.fragment.closest(element, selector)`: Finds closest matching ancestor.
- `up.fragment.config`: Configures defaults for fragment updates.
- `up.fragment.contains(root, query)` *(experimental)*: Whether root matches/contains selector/element.
- `up.fragment.etag(element)`: Returns ETag of content in element.
- `up.fragment.matches(fragment, selector, [options])`: Whether element matches selector.
- `up.fragment.onAborted(element, callback)` *(experimental)*: Callback when element/ancestors aborted.
- `up.fragment.source(element)`: Returns URL from which element loaded.
- `up.fragment.subtree(root, selector)`: List of descendants matching selector.
- `up.fragment.time(element)`: Last modification time of content.
- `up.fragment.toTarget(element, [options])`: Derives best-matching selector.
- `up.navigate([target], [options])`: Navigates to URL by updating major fragment.
- `up.visit(url, [options])`: Fetches URL and replaces main element with fragment.
- `up.template.clone(template, [data], [options])`: Clones template element.

### Events
- `up:fragment:aborted`: Requests for element aborted.
- `up:fragment:destroyed`: After fragment destroyed/removed.
- `up:fragment:inserted`: After fragment inserted/updated.
- `up:fragment:keep`: Before element kept during update.
- `up:fragment:loaded`: After server response loaded, before HTML changes fragment.
- `up:fragment:offline`: Device lost network during rendering.

---
## up.radio (Passive Updates)

### HTML Attributes
- `up-hungry`: Element updated whenever server sends matching element.
  - Example: `<div up-hungry>...</div>`
- `up-poll`: Element reloaded from server periodically.
  - Example: `<div up-poll="5s">...</div>`
- `up-flashes`: Shows confirmations, alerts, warnings.
  - Example: `<div up-flashes>Saved!</div>`

### JavaScript API
- `up.radio.config`: Configures defaults for passive updates.
- `up.radio.startPolling(fragment, [options])`: Starts polling element.
  - Example: `up.radio.startPolling(document.querySelector('.poll'))`
- `up.radio.stopPolling(fragment)`: Stops polling element.
  - Example: `up.radio.stopPolling(document.querySelector('.poll'))`

### Events
- `up:fragment:hungry`: Before `up-hungry` element added to render pass.
- `up:fragment:poll`: Before polling fragment reloaded from server.

---
## up.motion (Animation)

### HTML Attributes
- `up-transition`: Swaps fragment with animated transition.
  - Example: `<a href="/users" up-target=".list" up-transition="cross-fade">Show users</a>`
- `up-animation`: Animates overlay appearance.
  - Example: `<a href="/users" up-layer="new" up-animation="move-from-top">Show users</a>`

### JavaScript API
- `up.animate(element, animation, [options])`: Applies animation to element.
  - Example: `up.animate(document.querySelector('.box'), 'fade')`
- `up.animation(name, animation)`: Defines named animation.
  - Example: `up.animation('fade', { /* ... */ })`
- `up.transition(name, transition)`: Defines named transition.
  - Example: `up.transition('cross-fade', { /* ... */ })`
- `up.morph(oldElement, newElement, transition, [options])`: Animated transition between elements.
- `up.motion.config`: Sets default options for animations/transitions.
- `up.motion.finish([element])`: Completes animations/transitions.
- `up.motion.isEnabled()`: Returns whether Unpoly will perform animations.

### Events
- `up:motion:finish`: Emitted to request animation to finish instantly.

---
## up.status (Status Effects)

### HTML Attributes
- `up-nav`: Marks as navigation container.
  - Example: `<nav up-nav>...</nav>`
- `up-placeholder`: Placeholder shown while loading.
  - Example: `<div up-placeholder="Loading...">...</div>`
- `up-preview`: Names preview function called while loading.
  - Example: `<a href="/users" up-preview="showPreview">Users</a>`
- `up-alias`: Alternative URLs for highlighting as `.up-current`.
  - Example: `<a href="/users" up-alias="/people">Users</a>`
- `.up-current`: Link points to current location.
- `.up-active`: Origin element during rendering.
- `.up-loading`: Targeted fragments while loading.

### JavaScript API
- `up.preview(name, callback)`: Registers named preview function.
  - Example: `up.preview('showPreview', () => {/* ... */})`
- `up.status.config`: Sets default options for status effects.

---
## up.network (Network Requests)

### JavaScript API
- `up.request([url], [options])`: Makes AJAX request to URL.
  - Example: `up.request('/users').then(resp => { ... })`
- `up.network.abort([condition], [options])`: Aborts pending requests matching condition.
  - Example: `up.network.abort({target: '.list'})`
- `up.network.config`: Sets default options for network requests.
- `up.network.isBusy()`: Returns whether Unpoly is loading a request.
- `up.network.loadPage(options)`: Makes full-page request, replaces browser environment.
- `up.cache.alias(oldRequest, newRequest)` *(experimental)*: Cache aliasing.
- `up.cache.get(requestOptions)` *(experimental)*: Returns cached request.
- `up.ajax([url], [options])` *(deprecated)*: AJAX request and cache response.
- `up.cache.clear()` *(deprecated)*: Expires cache entries.
- `up.cache.evict([pattern])`: Evicts responses in cache.
- `up.cache.expire([pattern])`: Expires entries in cache.
- `up.network.isIdle()` *(deprecated)*: Returns whether Unpoly is not loading a request.
- `up.proxy.clear()` *(deprecated)*: Expires all cache entries.
- `up.proxy.preload(link)` *(deprecated)*: Preloads link.

### Events
- `up:network:late`: AJAX requests taking long to finish.
- `up:network:recover`: AJAX requests finished after delay.
- `up:request:aborted`: AJAX request aborted.
- `up:request:load`: Before AJAX request sent.
- `up:request:loaded`: After AJAX response received.
- `up:request:offline`: AJAX request encountered fatal error.

---
## up.event (Events)

### HTML Attributes
- `up-emit`: Emits custom event when element is clicked.
  - Example: `<button up-emit="my:event">Emit</button>`

### JavaScript API
- `up.on([element], types, [selector], [options], listener)`: Listens to DOM event.
  - Example: `up.on(document, 'up:link:follow', fn)`
- `up.emit([target], eventType, [props])`: Emits custom event.
  - Example: `up.emit(document, 'my:event', {foo: 1})`
- `up.event.build([type], [props])`: Builds event with type/properties.
- `up.event.halt(event)`: Prevents event from being processed further.
- `up.event.inputDevice` *(experimental)*: Class of input device for event.
- `up.event.onEscape(listener)` *(experimental)*: Listener for Escape key.
- `up.off([element], types, listener)`: Unbinds event listener.
- `up.$on` *(deprecated)*: jQuery-based event listener.
- `up.event.nobodyPrevents(eventType, eventProps)` *(deprecated)*: Emits event, returns if not prevented.

---
## up.protocol (Server Protocol)

### HTTP Headers
- `ETag`: Hash identifying content in response body.
- `If-Modified-Since`: Last modification time of fragment being reloaded.
- `If-None-Match`: ETag of fragment being reloaded.
- `Last-Modified`: Time when content in response body last modified.
- `_up_method`: Optional cookie echoing HTTP method.
- `Vary`: Request headers influencing response.
- `X-Up-Accept-Layer`: Accept targeted overlay in response to fragment update.
- `X-Up-Clear-Cache` *(deprecated)*: Control which cached responses expired after response.
- `X-Up-Context` *(experimental)*: Targeted layer's context (JSON).
- `X-Up-Dismiss-Layer`: Dismiss targeted overlay in response to fragment update.
- `X-Up-Events`: Emit events with requested fragment update.
- `X-Up-Evict-Cache`: Control which cached responses evicted after response.
- `X-Up-Expire-Cache`: Control which cached responses expired after response.
- `X-Up-Fail-Context` *(experimental)*: Context of layer for failed fragment update (JSON).
- `X-Up-Fail-Mode`: Mode of layer for failed fragment update.
- `X-Up-Fail-Target`: Target selector for failed fragment update.
- `X-Up-Location`: Set custom browser location after fragment update.
- `X-Up-Method`: Change HTTP method after fragment update.
- `X-Up-Mode`: Targeted layer's mode.
- `X-Up-Open-Layer` *(experimental)*: Force response to open new overlay.
- `X-Up-Origin-Mode` *(experimental)*: Mode of layer from which interaction originated.
- `X-Up-Reload-From-Time` *(deprecated)*: Timestamp of existing fragment being reloaded.
- `X-Up-Target`: Read/change target selector for fragment update.
- `X-Up-Title`: Change document title after fragment update.
- `X-Up-Validate`: Names of form fields being validated.
- `X-Up-Version`: Current Unpoly version for fragment update.

### JavaScript API
- `up.protocol.config`: Configures strings for server protocol.

---
## up.dom / up.element (DOM Helpers)

### HTML Attributes
- `hidden` *(experimental)*: Hides element from page.
  - Example: `<div hidden>...</div>`

### JavaScript API
- `up.element.affix(parent, [position], selector, [attrs])`: Creates element and attaches to parent.
- `up.element.attr(element, attribute)`: Returns attribute value for element.
- `up.element.booleanAttr(element, attribute)`: Returns boolean value of attribute.
- `up.element.createFromHTML(html)`: Parses element from HTML string.
- `up.element.createFromSelector(selector, [attrs])`: Creates element matching selector.
- `up.element.createNodesFromHTML(html)` *(experimental)*: Parses list of nodes from HTML.
- `up.element.get([parent], value)`: Returns native Element for value.
- `up.element.hide(element)`: Hides element.
- `up.element.isEmpty(element)` *(experimental)*: Returns whether element has no content.
- `up.element.isVisible(element)`: Returns whether element is visible.
- `up.element.jsonAttr(element, attribute)`: Reads attribute as relaxed JSON.
- `up.element.numberAttr(element, attribute)`: Returns attribute value as number.
- `up.element.setAttrs(element, attributes)`: Sets object properties as attributes.
- `up.element.setStyle(element, styles)`: Sets CSS properties as inline styles.
- `up.element.show(element)`: Shows element.
- `up.element.style(element, propOrProps)`: Gets computed CSS styles.
- `up.element.styleNumber(element, prop)`: Gets computed CSS property as number.
- `up.element.subtree(root, selector)`: List of descendants matching selector.
- `up.element.toggle(element, [newVisible])`: Changes whether element is shown/hidden.

### Deprecated
- `up.element.all`, `up.element.closest`, `up.element.first`, `up.element.isAttached`, `up.element.isDetached`, `up.element.matches`, `up.element.remove`, `up.element.replace`, `up.element.toggleClass`, `up.element.toSelector`

