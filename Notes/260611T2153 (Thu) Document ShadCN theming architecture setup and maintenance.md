

## Overview
Setup documentation, process, agent-skills and rules around theming and styling setup and maintenance
- How the current theme architeture is setup (or is supposed to be setup as its all WIP)
- What styles are useful for what times. Pair the styles for background and text. i.e. `bg-primary/text-primary-foreground` pair.
	- Use the `client/documentation/theming-archture/*.md` docs

## Tasks
- `primary` tokens are used too often. It should be reserved for the primary brand color.
	- Buttons are using primary as dark/light color. The variant can stay "primary" but the color tokens inside should not be based on primary. Otherwise there'd be too much use of primary
	- Components should be upgraded to through shadcn cli, and any customization on existing (legacy) components should be copied over to them. For example, if a new custom variant is added in the current `Button` the new updated `Button` component should be updated as well.
		- Especially use the Sidebar Component from the ShadCn.
		- Use new tab components which support the different styles for tabs, by default (no custom styling required)
		- Use Select, Autocomplete components from updated ShadCn library. (**Or use ShadCn Studio instead**)
	- Attempt to go shadow-less or as low shadows as possible.
	- 




---



## Useful Resources
- [Making Sense of Shadcn UI's Theming and Color Variables](https://isaichenko.dev/blog/shadcn-colors-naming/)
- [ShadCN Guidelines - Cli, Rules & Skills](https://github.com/shadcn-ui/ui/blob/main/skills/shadcn/rules/styling.md)
- Use the following images based on AI Search Results of **[how to use different theming variables from shadcn like muted, primary, foreground, card etc](https://www.google.com/search?q=how+to+use+different+theming+variables+from+shadcn+like+muted%2C+primary%2C+foreground%2C+card+etc&client=ubuntu-sn&hs=Uan&sca_esv=dd2fe0b82f78cb75&channel=fs&sxsrf=ANbL-n6VBQw5zdnumfbli5TA7R0dOJGoNw%3A1781196346635&ei=OuYqatKpJpqckdUP-Y-AmQ0&biw=2084&bih=1041&ved=0ahUKEwjSrpC80f-UAxUaTqQEHfkHINMQ4dUDCBA&uact=5&oq=how+to+use+different+theming+variables+from+shadcn+like+muted%2C+primary%2C+foreground%2C+card+etc&gs_lp=Egxnd3Mtd2l6LXNlcnAiXGhvdyB0byB1c2UgZGlmZmVyZW50IHRoZW1pbmcgdmFyaWFibGVzIGZyb20gc2hhZGNuIGxpa2UgbXV0ZWQsIHByaW1hcnksIGZvcmVncm91bmQsIGNhcmQgZXRjSKCaAlCVB1jtmAJwBngBkAEAmAGUAqABl7UBqgEHMC4xOS44NbgBA8gBAPgBAZgCRqACuHzCAgoQABhHGNYEGLADwgIFECEYoAHCAgUQIRifBcICBxAhGAoYoAHCAgoQIxiABBiKBRgnwgIEECMYJ8ICCxAAGIAEGIoFGJECwgILEAAYgAQYsQMYgwHCAgUQABiABMICDhAAGIAEGIoFGLEDGIMBwgIREC4YgAQYigUYkQIYxwEYrwHCAhEQLhiABBixAxiDARjHARjRA8ICCxAAGIAEGIoFGLEDwgIIEAAYgAQYsQPCAgUQLhiABMICBBAAGAPCAgYQABgWGB7CAgcQABiABBgNwgIGEAAYHhgNwgILEAAYgAQYigUYhgPCAgUQABjvBcICBhAhGBUYCsICBBAhGBXCAgQQIRgKmAMAiAYBkAYIkgcGMi41LjYzoAfrwAOyBwYwLjUuNjO4B698wgcHMS4zMS4zOMgHuQGACAE&sclient=gws-wiz-serp)**
	- ![[how to use different theming variables from shadcn like muted, primary, foreground, card - pt1.png]]
	- ![[how to use different theming variables from shadcn like muted, primary, foreground, card - pt2.png]]
	- ![[how to use different theming variables from shadcn like muted, primary, foreground, card etc - pt3.png]]
