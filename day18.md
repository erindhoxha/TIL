## Day 18

Today I dove deeper into AI agents, flows, and skills, and I discovered some powerful ways to modularize and scale
knowledge across projects. One thing that stood out is how we can target separate projects with specific skills, which
allows agents to be highly specialized depending on the project context.

I didn't know that we could target separate projects with skills. A good example is here:

https://vercel.com/blog/introducing-react-best-practices

By running `npx add-skill vercel-labs/agent-skills`

It shows in the terminal which skills you want the agent of that project (or global!) to learn:

- Composition Patterns – Best practices for composing React components effectively
- React Best Practices – Guidelines for clean, maintainable, and performant React code
- React Native Skills – Mobile-specific React patterns and optimizations
- Web Design Guidelines – UX, accessibility, and design standards

Then we can choose with which model, e.g. Claude Code, Copilot etc.

It then creates a couple folders and files in the places we decided to go in, e.g. .github/skills or .claude/skills.

We can then hide these in .gitignore.

I’m also starting to see the potential for flows, where agents can chain skills together for more complex multi-step
tasks. For example, one flow could use a React Best Practices skill to review code, then a Composition Patterns skill to
suggest optimizations, and finally a Web Design Guidelines skill to check accessibility compliance, all automatically.
