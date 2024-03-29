Things I've worked on during my time at RevenueHero

#### Mentors
- @jartek
- @VarunNatraaj
- @pranav91
- @Reyzartz
- @anandrhdes

#### Areas
- UI
	- React
		- UI components with styling
		- modifying JSX children, JSX tree parsing
		- UI render optimisations
	- Astro
		- contributed to RevenueHero public-scheduler
		- restructured the codebase
		- made optimisations with help from @jartek to improve loading speed of the scheduler
		- primary attention 
			- lazy loading
			- network waterfalls
	- Svelte
		- contributed to RevenueHero meeting-links
		- migrated the app from Astro to SvelteKit
		- optimised it to load super fast as its a SPA
	- Web components/ Custom Elements
		- built some web components to make custom form validation work with native forms
- REST APIs
	- Fastify, Postgres, Objection + Knex.js, Playwright, BullMQ
		- REST API endpoints
		- Postgres DB with Objection + Knex ORM
		- Queues and background job processing
		- Unit Tests with Node-TAP (first time) (200 + tests) (guide @jartek)
	- Rails
		- Learning ruby and wrote a tiny part of main API under guidance of @jartek
- Tests (first time)
	- Cucumber.js, Playwright
		- Wrote the RevenueHero E2E Test Framework under guidance and idea of @jartek
		- A powerful framework that makes it possible to write tests as UI, with reusable test components
		- Written in TS (JS) OOP (first time)
		- Spent 2-3 months
		- The framework is fully typed, with automatic data creation
- Theming (first time)
	- Implemented color computation logic under guidance and idea of @anandrhdes
	- This involved handling a lot of edge cases regarding colour contrast, look and feel of UI etc.
- Chrome Extensions
	- multiple chrome extensions based on react
	- worked on fixing issues with react rendering and styling of injected content scripts
- npm package and bundling
	- extensively worked on package bundling
	- multiple transpilers, rollup setup, tree-shaking etc