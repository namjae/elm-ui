# 0.4.0
This release is for upgrading to Elm 0.18.

### Changes
* Added the option `-d, --debug` to turn on Elms debugger.
* Using `yarn` instead of `npm` internally.
* Fixed braking changes.


# 0.3.0
This is the release comes with may improvements to the workflow and coincides
with the release of the official website that provides guides and documentation.

## Breaking Changes

### Removing `elm-ui.json`
The `elm-ui.json` file was created in order to use Elm-UI without it being in
the official repository, this caused some confusion for people, but there was
no other way around it at the time, this is now however changed so the file
became unnecessary, (you can read more about it below) so make sure
that after you upgrade, to remove it from your projects.

### Installing packages
A custom package resolver and installer has been implemented that has mostly
the same functionality as the official installer (`elm-package`) and the added
functionality to **install packages directly from Github**, that means that Elm-UI
can be installed as any other standard package (from the CLI).

You can read more about it here https://github.com/gdotdesign/elm-github-install

### Changes
* The environment files are always read when compiling an file, so there are
  no server restarts are necessary
* Migrated specs from intern to nightwatchjs and they are running again on Travis on Chrome and Firefox
* Removed Ui.Native.Dom in favor of the official Focus library
* Added Ui.Helpers.Ripple - A module to add ripple effect when clicked
* Added Ui.Native.Uid - A module to generate unique ids without tasks
* Added Ui#link - A way to create unobtrusive links
* Added Html.Events.Extra#unobtrusiveClick - A unobtrusive way to handle click
  events on **a** tags
* Ui.Header - It has been redesigned to use records instead of parameters
* Ui.Layout - It has been redesigned to be more developer friendly and less
  confusing
* Ui.FileManager - The way to get files have been changed to use a Decoder and
  a Task instead of just a Task
* Ui.Tagger - Fixed a bug in where readonly tags would have "x" icon

# 0.2.2
Bugfix release.

# 0.2.0
This version marks support for Elm 0.17 with many changes to make Elm-UI more accessible.

## Breaking Changes

### Index.html
The index.html is now served from `public` directory to make it more accessible and allow people to easily add CSS and third party JavaScript to their applications.

### Singals Removal
Because of the removal of Signals the way how components receive changes from sub components is changed from using a `valueAddress` to having a subscription of changes.

Before
```elm
  ...
  {- This made sure that we receive changes form
     the input on the Changed action
  -}
  input = Ui.Input.initWithAddress Changed "value" "placeholder"
  ...
```

Now
```elm
  ...
  {- Initialize an input like normal. -}
  input = Ui.Input.init "value" "placeholder"

  ...

  {- Subscribe to the changes with a subscription. -}
  subscriptions: (\model -> Ui.Input.subscribe Changed model.input)
  ...
```

This works because of the **Ui.Helpers.Emitter** module.

## Log
### New Components
- **Ui.Layout** - A component for rendering commonly used layouts

### Changes
- Signal related modules are removed (Ext.Signal)
- All files are now formatted with **elm-format** (2 space indentation)
- **Browser** native module have been separated into 3 modules:
  - **Browser** - Browser related functions (alert, redirect, openWindow)
  - **Dom** - DOM related related functions (focus, blur)
  - **Number** - Number related functions (toFixed, rem)
- **Ext.Color** - Added **encodeHsv** and **decodeHsv** functions
- **Html.Extra** module have been cleaned up and separated into 3 modules:
  - **Html.Events.Extra** - Extra event handlers
  - **Html.Events.Geomtery** - Functions and decoders for getting HTML Element dimensions
  - **Html.Events.Options** - Extra options for event handlers
- **Storage.Local** module have been renamed to **Ui.Native.LocalStorage**
- **Ui.Utils.Env**:
  - Have been renamed to **Ui.Helpers.Env**
  - **get** changed to return a result instead of requiring a default value
  - Added **getString** to get string values easily
- Removed **Ui.Helpers.Animation** module
- Removed **Ui.Charts.Bar** module
- Added **Ui.Helpers.Emitter** module (pub / sub) to send values to different channels
- Added **Ui.Native.Browser** module to interface with it's native module
- Added **Ui.Native.Dom** module to interface with it's native module
- Added **Ui.Native.Scrolls** module to get the scroll events from window
- Added **Ui.Native.FileManager** module to manage files
- **Ui.Tagger** - Simplified implementation
- And many small changes...

### Style Changes
- Changed the all the colors
- The cursor for readonly and disabled states are more "descriptive"
- The readonly focus color is the same as the not readonly one
- The style of **Ui.NumberPad** changed to be more in line with the theme
- The style of **Ui.Tabs** changed to be more in line with the theme
- The style of **Ui.Slider** changed to be more in line with the theme
- The focus style of **Ui.Button** changed to show a "ripple effect"
- And many small changes...

# 0.1.5

## Pull Requests Closed
- [Changing mgold's elm-date-format dependency for more powerful rluiten…](https://github.com/gdotdesign/elm-ui/pull/17)
- [Fix typo in README](https://github.com/gdotdesign/elm-ui/pull/15)
- [Fix typo in documentation](https://github.com/gdotdesign/elm-ui/pull/14)
- [Fix documentation for iconAttributes](https://github.com/gdotdesign/elm-ui/pull/13)
- [Tabs +1](https://github.com/gdotdesign/elm-ui/issues/20)

## New Components
- **Ui.Tabs** - A component to handle tabbed contents
- **Ui.scrolledPanel** - A static component for scrollable content (scrollbar styled for Chrome)

## Changes
- Now using **elm-date-extra** for date formatting instead of **elm-date-format**
- Unified how values are set for components with **setValue**:
  - **Ui.Chooser.select** renamed to **Ui.Chooser.setValue**
  - **setValue** functions no longer send the given value to the valueAddress
  - Added **setAndSendValue** to some components
- Header componets are moved into a seprate module:
  - **Ui.header** is now **Ui.Header.view**
  - **Ui.headerIcon** is now **Ui.Header.icon**
  - **Ui.headerTitle** is now **Ui.Header.title**
  - Added **Ui.Header.separator**
  - Added **Ui.Header.item**
  - Added **Ui.Header.iconItem**

## CLI
- Added **docs** command to generate Elm documentation.
- Added **start** alias for **server** command.
- Environment data and Elm app initialization is now bundled into JS file

## Ui.Container
- **render** function is now exposed

## Ui.Input
- Added **focus** function to focus a **Ui.Input** component

## Ui.Textarea
- Added **focus** function to focus a **Ui.Textarea** component

## Ui.Tags
- Added ability to tab to the remove icons

## Html.Extra
- Added **onWheel** event handler
- Added **deltaDecoder** to decode wheel deltas

## Native.Browser
- Changed how DOM elements are accessed internally
- Added **haveSelector** function to check for an element in the DOM
- Added **atElement** decoder which tries to find the first child element with the given selector
- Added **closest** decoder which tries to find the closest element with the given selector
- Added **focusTask** to focus an element with the given selector as a Task

## Native.LocalStorage
- Changed it to use Task instead of Result
- Added support for [chrome.storage](https://developer.chrome.com/extensions/storage) storage.

# 0.1.3

## New Components
- **Ui.ButtonGroup** - A component for handling multiple buttons together
- **Ui.Tagger** - A component for managing tags on an entity
- **Ui.Time** - A component for displaying relative time
- **Ui.Loader** - A loader component (with a timeout before showing)
- **Ui.SearchInput** - A component for handling text search
- **Ui.breadcrumbs** - A component for displaying breadcrumbs navigation
- **Ui.headerIcon** - Added to be used in specifically in **Ui.header**

## Component Changes
- **Ui.text** is now **Ui.textBlock** to avoid collision with **Html.text**
- Added remaining variations to **Ui.Container**
- Providing a placeholder for **Ui.Icon** is now mandatory
- Switched the **viewModel** and **address** parameters in **Ui.NumberPad**
  to be more consistent with the other components
- Changed the default colors for **success, danger** and **warning**

## Fixes
- Fixed an issue with Safari slowness #5
- Fixed an issue that prevented Elm-UI from working in Safari
- Fixed **Ui.Choosers closeOnSelect** behavior when pressing the **enter key**
- Optimized rendering of many components
- Optimized rendering of the KitchenSink demo (~5ms down from ~16ms)
