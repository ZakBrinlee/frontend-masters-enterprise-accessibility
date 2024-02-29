# Frontend Masters Course - Enterprise Accessibility

## What will be covered

- Intro
- Mimimum Viable Products
- Accessible UIs
- Accessible Naming & Screen Reading Concerns
- Accessibility in JS Apps
- Test Automation for Accessibility
- Organizational Skill-Building
- Wrap up

## Questions

- How important is A11y on mobile?
  - Very. Many use cases such as bluetooth keyboards, touch targets larger, etc

## Links

- [Business Case for Digital Accessibility](https://www.w3.org/WAI/business-case/)
- [Accessibility with Animations - FEM course section](https://frontendmasters.com/courses/svg-essentials-animation/accessibility/)
- [Examples of accessibility personas](https://enterprise-accessibility.vercel.app/topics/mvps/a11y-personas#examples-of-accessibility-personas)
- [Accessible Name and Description Computation](https://www.w3.org/TR/accname-1.2/) -standardizes the process of choosing accessible names so we don’t encounter absolute chaos across platforms.
- [What we learned from user testing of accessible client-side routing techniques with Fable Tech Labs](https://www.gatsbyjs.com/blog/2019-07-11-user-testing-accessible-client-routing/)
- [What Input library](https://github.com/ten1seven/what-input) - A global utility for tracking the current input method (mouse, keyboard or touch).
- [React Refs](https://react.dev/learn/referencing-values-with-refs)
- [Understanding Assistive Technologies: What Are Sip-and-Puff Systems?](https://www.boia.org/blog/understanding-assistive-technologies-what-are-sip-and-puff-systems)

## Intro

- Enterprises really cannot afford to not address digital accessibility in their products
- Best effort to catch "accessibility misses" as much as we can
- Goal of the Workshop
  - Understanding the core requirements for digital accessibility in the enterprise.
  - Tech leads should be able to advise team members how to produce accessible, quality software.

## Mimimum Viable Products

- Incorporate A11y into planning and design as early in a a project process as possible
- Do less, IF you can't make it accessible
- What kinds of items needs to be addressed in Design?
  - Headings, Buttons, Links, Forms, Focus, Menus
- Consider audience when needing to convince stakeholders.
  - Carrot or Stick approach. Find the business gains
  - **Accessibility impact of issues**, including WCAG success criteria and level. _Does this significantly block users?_
  - **Analytics and metrics**. Are core user flows impacted? Which browsers and platforms?
  - **Identify areas needing more help**. Do we need design thinking or content strategy to get this right?
  - **The cost of not doing it.** I’m no MBA but I could take a pass on estimating the cost of a retrofit vs. doing something right from the start if I broke it down into parts.
- Understand accessiblity personas!

## Accessible UIs

- Design with access in mind: visual contrast, font size, icons that are easy to understand, intuitive interactive interfaces, and more
- Fundamental foundation -> **semantic markup with HTML**
- ARIA -> standard set of role, state and property attributes that target Assistive Technology.
- Structure with headings and landmarks - semantic structure
  - `<h1>-<h6>`
  - `<main>, <nav>, <footer>, <section>` and more
  - content markup -> `<ul>` and `<ol>`
  - using the correct elements for interactivity with keyboards and screen readers
- What makes the A11y spidey sense go off?
  - Form labels made with `<spans>` -> easy to change to a `<label>` element (aria label on input won't make visible text)
  - Custom controls on forms -> custom dropdown, `<select>`, `<date-picker>`, typeahead
  - Colors! -> color contrast should be addressed, if you see blending between text/background its a big issue
  - Modals and Layers -> sending/restoring focus, keyboard trapping, using `dialog` role, focusable and labeled buttons and CTAs
  - Mouse only interactions -> `onClick` handler on a `div`
- Visibility Methods
- Custom CSS classes for handling visibility of elements that still need to be visible to screen readers
  - `.visually-hidden`, `.sr-only`: renders element invisible but readable from SR
  - `display: none` in CSS: hides content from everyone. Keyboard users, SR users, sighted mouse users, and all (animatable with keyframe)
  - `visibility: hidden` in CSS: renders element invisible, hidden from keyboards and SRs. Reserves visual space within the rendered layout (animatable with keyframe)
  - `opacity: 0`: renders element invisible BUT keeps it accessible to keyboards and SRs. (animatable)
  - `aria-hidden`: Will not affect render functionality, but will impact screen-readers. Will mark the content to ignore from SRs and will still maintain focus/accessible elements inside (great for hiding icons from SR)
  - `hidden` attribute in HTML: Same effect as CSS `display:none`
- How to Test UI Components
  - 1. Use keyboard to TAB through a page and look for reading components, interactive control, compound widgets
  - 2. Run a browser extension like Axe or Accessibility Insights
  - 3. Zoom in to at least 200% to ensure the pages reflow without horizontal scrolling
  - 4. Test with screen reader (SR)
  - 5. Check that animation, motion, and autoplaying videos can be turned off with controls/Reduced-Motion settings
  - 6. Make note of any media in need of captions, transcripts, or alt content
  - 7. Bake it into the code with automation testing like Cypress-Axe

## Accessible Naming & Screen Reading Concerns

- HTML form controls have names. Links and buttons have names. Section elements and tables have names, as well as other elements. (DIV elements do not.)
  - `aria-labelledby` -> then `aria-label` -> then `title/placeholder` or form `<label>`
- HTML Descriptions
  - announced in SRs, but they come with a delay and are configurable (users may not always hear the descriptions)
- Perfer visible text over using `aria-label`
- Utilize Chrome DevTools accessiblity inspector

### Acessiblity Tree

- Parallel structure to the DOM to surface accessiblity info to Assistive Technology
- Accessiblity viewer using Chrome DevTools. Super helpful
- By learning about the accessibility tree and how it relates to the DOM, you’ll have a better understanding of what ARIA is and how it relates to HTML.

### Testing a Given ARIA Solution

- Tips for testing ARIA solutions
  - 1. Compare your site’s analytics to the [WebAIM screen reader surveys](https://webaim.org/projects/screenreadersurvey9/) to know what screen reader and browser combinations people actually use. This can help you prioritize.
  - 2. People who use screen readers regularly. We’ll talk about this more in organizational skill building.
  - 3. Check [A11ySupport.io](https://a11ysupport.io/) for specific attribute support.
  - 4. The ARIA Authoring Practices might have some suggestions, although these are not production ready.
  - 5. Snoop around issue trackers for the major repos: [NVDA](https://github.com/nvaccess/nvda), [WAI-ARIA](https://github.com/w3c/aria), [WCAG](https://github.com/w3c/wcag), [WebKit and Safari](https://bugs.webkit.org/), and more.)
       - Go through the archives of the [WebAIM email discussion list](https://webaim.org/discussion/archives) and ask a new question if needed.
- Screen readers are NOT the only thing in accessiblity
  - Remember to test keyboard support, visual contrast, reflow & zoom, navigating by voice, and more
  - Think about Skip Links, both for visual users and SRs

### Visual and Non-visual experiences

- Utilize crafting the non-visible exp with semantic structure and content
- Clear visual contrast, readable fonts, zoomable pages, and more

### Screen Reader Commands & Interaction Modes

- Awesome tips/commands for using Screen Readers on different devices
  - [Screen Reader command cheatsheet](https://enterprise-accessibility.vercel.app/topics/accessible-naming-screen-readers/screen-reader-commands-interaction-modes)
- Windows screen readers also have a concept of [interaction modes](https://tink.uk/understanding-screen-reader-interaction-modes/) that higher-level engineers should know about.
  - Default mode in NVDA, for example, is Browse Mode. This allows reading of content and cycling through headings with the H key, for example.
  - When you focus in a form input or contenteditable widget, the mode changes to Forms Mode a.k.a. Focus Mode.
  - You can also swap modes manually using the key command NVDA + Space (where NVDA is the Insert key on a Windows keyboard, unless it has been mapped to something else).
- There is also the ARIA application role that puts a user directly into Focus mode. Be VERY careful about using this as you will essentially strip away Windows screen reader commands and keystrokes will be passed directly to the browser.

## Accessibility in JS Apps

### Client-side Rendering and Routing

- ScreenReaders use JavaScript to function
- Don't need to support non-JS to be accessible
- Consider lower-bandwidth networks and older devices for people with disabilities.
- JS handles routing page to page without a page refresh, this impacts on keyboard focus and SR exp, as the typical page title announcements and focus won't reset unless we actively replace them
- There are multiple techniques to handle client-side routing for accessibility:
  - Send focus to the main heading (with tabIndex="-1" on it) in the new content so it is announced and focus doesn’t remain on the old content.
  - Send focus to a wrapper element with the new content (also with tabIndex="-1" on it).
  - Mark up the new content itself with an ARIA Live Region so it’s announced on change and leave focus where it is.
  - Make an ARIA live region announcement on an .sr-only element and leave focus where it is.
- Techniques to handle page transition focus:
  - 1. Move focus to the new content to put users in the right part of the page.
  - 2. Make a Live Region announcement so the page change is explained.
  - Codepen demo: https://codepen.io/marcysutton/pen/VwzdBQJ

### Managing Focus in Interactive Components

- Common focus management patterns in JS apps
  - Modals and view changes.
    - We must move focus into the modal content on open and restored on close.
    - Modal layers should also prevent interaction in the background.
  - Tab switchers and date pickers.
    - Using [roving tabindex](https://www.w3.org/WAI/ARIA/apg/patterns/radio/examples/radio/), we can create one focusable control that enables the arrow keys for interaction inside the component.
  - Add/delete of items.
    - Depending on the browser, deleting a node while focused can kick the user back to the top of the page...not very ergonomic. Instead, we should handle focus when items are deleted and containers re-rendered.
  - Other interactive widgets.
    - There are others. Think like a keyboard user who doesn’t want to get stuck behind layers or who can’t reach content they can see on screen.
- When to show a focus outline
  - Any time you use the TAB key to reach an interactive control like a button, link, form input, tab switcher, etc., there needs to be a visible focus style
  - Check out the `:focus-visible` pseudo-class to make your life easier in this regard

### Semantics & ARIA in JS Apps

- Learn the default HTML elments, attributes and properties
- Use headings, landmarks, lists, figures, data tables and more to add semantic structure to your pages. These are essential for users of Assistive Technology to navigate and digest web page content.
- Use buttons and links for their intended purposes. For buttons, this means toggling UI components and being part of forms. Links are for navigation! Links also require an href attribute to be keyboard accessible.
- Make sure you understand ARIA before using it
- It helps to follow the rules of ARIA and test it regularly:
  - 1. If you can use a native HTML element or attribute with the semantics and behavior you require already built in, instead of re-purposing an element and adding an ARIA role, state or property to make it accessible, then do so.
  - 2. Do not change native semantics, unless you really have to.
  - 3. All interactive ARIA controls must be usable with the keyboard.
  - 4. Do not use role="presentation" or aria-hidden="true" on a focusable element.
  - 5. All interactive elements must have an accessible name (hey, we know that one!).

### What to look for in a framework

- When choosing JS framework, consider the following for A11y
  - 1. Support for semantic HTML and ARIA.
       - Does the framework get in your way when creating accessible markup? Most of the libraries have gotten very good at this - you can include ARIA attributes with ease and many have accessibility features. But they also don’t necessarily discourage you from putting click events on DIVs. Just sayin’.
  - 2. Routing
       - Does your routing library do anything for client-side routing and accessibility? This has been difficult enough in my experience to recommend multi-page apps over client-side routing. But you could also check out the Navigation API.
  - 3. Docs and Community
       - Do a search of the docs and code repos for the library. Have they handled accessibility issues well? Is there a culture around making accessibility improvements, or have issues languished for half a decade (or been closed with no action)?
  - 4. Testing Tools
       - Testing tools are super helpful to have. You can always bolt on an agnostic testing framework like Cypress. But other tooling for your particular library (like Jest, Testing Library, etc.) will prove to be essential for any long-lived web application.
- Some other considerations when picking a library or framework:
  - What is the potential lifespan of your project? Will you need something super robust for years to come, or is it for a smaller project that has fewer requirements?
  - What is the funding model of the framework you’re considering? Were they just acquired, and by whom?
  - Who is maintaining it and what is the state of their issue tracker/codebase for accessibility?

### Hybrid App 101

- It’s best to focus on creating a good user experience. Can someone with a Bluetooth keyboard reach and operate every interactive control (sound familiar)? Can a screen reader user understand where they are on the screen and complete tasks without assistance?
- While you could test webviews within a native app on their own using regular web testing tools (and your keyboard and screen readers), any tools for testing native mobile apps will apply for hybrid mobile apps:
  - https://developer.apple.com/library/archive/technotes/TestingAccessibilityOfiOSApps/TestingtheAccessibilityofiOSApps/TestingtheAccessibilityofiOSApps.html
  - https://developer.android.com/guide/topics/ui/accessibility/testing
  - https://docs.deque.com/devtools-mobile/2023.8.16/en/intro
  - https://www.evinced.com/products/flow-analyzer-for-mobile

## Test Automation for Accessibility

### How Accessibility Guidelines Fit into Automation

- What can be automated
  - HTML/ARIA validation
  - Form labels
  - Color contrast
  - Accessible names
  - Focus management
  - Specifying a language
- What needs to be manually tested
  - Focus order
  - Text alternative quality
  - Screen reader testing
  - Contrast over images/gradients
  - Error identification
  - Click events on DIVs
- Tests can be tailored for aspects that can be automated, like keyboard support, ARIA states, labels, and more.
- Automated A11y testing is about striking the right balance of automation, reliable code patterns, QA, and persistence

### Appraches for Testing

- Unit testing for isolated logic and functionality
- component testing for a single component or a group of components
- integration testing for compound components or pages
- end-to-end testing for whole pages
- Linting
  - You can run accessibility tests in your text editor (many of us use VS Code these days) using [ESLint-Plugin-JSX-A11y](https://www.npmjs.com/package/eslint-plugin-jsx-a11y).
  - There is also [Axe Linter](https://www.deque.com/axe/devtools/linter/) which uses the same engine as axe-core and the Axe browser extensions.
- Unit tests
  - [Jest](https://jestjs.io/) is the modern standard for most unit tests in web apps these days. There are excellent tools to use with Jest for accessibility testing, including [Jest DOM](https://github.com/testing-library/jest-dom) with its accessibility matchers.
  - [Testing Library](https://testing-library.com/) has become essential for accessibility testing with its queries and userEvent API Testing Library. It also includes framework APIs for vanilla DOM, React, React Native, Vue, Angular, Preact, Svelte, Cypress, Puppeteer, and more.
- Component testing
  - Within automated testing, [Cypress Component Testing](https://docs.cypress.io/guides/component-testing/overview) is also worth considering. If you already use Cypress and you like their API, you could use it to isolate single components or groups of components using the Cypress API. This is opposed to testing whole pages, to which regular Cypress is well suited.
  - Don’t sleep on [Storybook](https://storybook.js.org/) for component testing. It bridges the gap between manual testing and automated testing, and can be essential for some teams. You can build out your components, variants, data states, and more in Storybook and test them with ease.
- Integration testing
  - After unit testing, integration testing is the next big leap. Both integration and end-to-end testing can assert more real-world browser testing, document/page-level rules, widget interoperability, and color contrast. They also offer more flexible framework testing options.
  - Integration testing is often done with Cypress or [WebdriverIO](https://webdriver.io/), although Jest tests can blur these lines quite a bit (as can WebdriverIO!). The goal is to bring multiple components together in test and ensure there aren’t any unexpected effects.
- Configuring Testing Tools
  - Here are some questions to ask while configuring tooling:
    - How is the UI in your app rendered? React-DOM, React-Native, Angular, etc.?
    - Can you inject tooling for accessibility tests in that context?
    - i.e., can you inject Axe into the target document or environment?
    - How is the code bundled?
    - Does it use webpack, Parcel, etc.?
    - Can you make changes to the infrastructure for accessibility testing, or will you have to make do with what’s already there? (i.e. Testing Library userEvent)
    - Who do I have to talk to to get a configuration change around here? 😏
  - Links
    - https://jestjs.io/
    - https://testing-library.com/
    - https://github.com/testing-library/jest-dom
    - https://docs.cypress.io/guides/component-testing/overview
    - https://storybook.js.org/
    - https://cypress.io
    - https://webdriver.io/

### Continous Integration (CI)

- Continuous integration is a DevOps software development practice where developers merge code together in a central repository, after which automated builds and tests are run
- CI that runs on every PR and build can help to encourage testing on more platforms, prevent regressions, and enable a culture of test coverage
- It’s better to configure automated test tooling to meet your needs in various test flows than to disable accessibility tests entirely.

### Using an A11y Testing API

- The [axe-core library](https://github.com/dequelabs/axe-core) has become popular because it has solid results and it’s free and open source. You can integrate it into unit tests, although its page-level rules for contrast in particular could be quite slow. You might want to limit it to integration or end-to-end testing where you can run the API on a larger section of DOM for performance reasons.
- There are different flavors of Axe that could be useful:
  - [@axe-core/react](https://www.npmjs.com/package/@axe-core/react)
  - [Jest-axe](https://www.npmjs.com/package/jest-axe)
  - [Cypress-axe](https://www.npmjs.com/package/cypress-axe)
- An accessibility test API can help you with:
  - HTML nesting and structuring issues
  - Label/name computation
  - Incorrect ARIA usage
  - Color contrast
  - Data table markup
  - Viewport/zooming problems

## Organizational Skill-Building

### Tips for Building Institutional Knowledge

- We can help each other, our companies, and our products by bringing our minds and perspectives to the table and increasing [institutional knowledge](https://www.oneil.com/the-importance-of-documenting-institutional-knowledge-six-benefits-for-your-organization/).
- Here are some tips for increasing cultural awareness of accessibility in an organization:
  - Conduct testing with people with disabilities, and share the recordings. Nothing hits quite the same as watching someone struggle touse your product. [Fable](https://makeitfable.com/) is one company that does this.
  - Put an [Accessibility Statement](https://www.w3.org/WAI/planning/statements/) on your website and share feedback with teams.
  - Include accessibility documentation in easy-to-find places, such as testing tips and user keyboard shortcuts.
  - Schedule lunch & learns or similar presentations. Even recorded ones on the internet could make great sessions!
  - In office? Hang accessibility tips in the bathroom stalls.
  - Talk about accessibility in planning, design, and code reviews.
  - Make everyone responsible for it, not only the accessibility team (or lone specialist).
  - Take care in terms of burnout. It’s unfortunately common in accessibility. Find sustainable improvements you can make that bring joy and job satisfaction.

### Working with Larger Codebases

- Utilize core components with accessibility baked in
- Centralize UI components for reuse using design systems and core component libraries, whether by building your own or using a third-party library, it can provide opportunities for accessibility (or challenges, depending on the library).
- Gather perspective for a bigger picture on team
- Make accessibility easy to test
- Look for accessibility documentation including testing steps, or create some
- Use consistent accessibility test rules and processes
- Talk to your teammates / code authors to understand their approach
  - Identify areas for improvement, risks and challenges, or simply a better understanding of how things work at your organization.

### Inclusive Hiring & Workplaces

- Ensure there aren’t discriminatory tools or practices keeping people with disabilities out

### Centering People with Disabilities

- People with disabilities should be involved in design and development as often as possible–there is a rich activist history around this idea.
- Advocating for people with disabilities in design and development
- Look for perspectives and personas of people with disabilities when you read through accessibility specs, guidelines, and W3C GitHub repos for WCAG and ARIA to understand how something might affect users

### The Definition of Done

- Make it a requirement that’s documented in tickets, stories, issues, etc
- Including accessibility as acceptance criteria can help to surface it at a good time: before something has shipped.
- Make it an actual requirement
- Teams first have to know that accessibility is a requirement and then know how to test it! Checklists are a starting point. But having a repeatable, shareable process for accessibility testing will be a lot more impactful than none.
- Include accessibility in performance reviews (and interviews)
