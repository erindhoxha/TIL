## Day 18

I learned more about AI, Agents, Flows, Skills.

I didn't know that we could target separate projects with skills. A good example is here:

https://vercel.com/blog/introducing-react-best-practices

By running `npx add-skill vercel-labs/agent-skills`

It shows in the terminal which skills you want the agent of that project (or global!) to learn:

- Composition Patterns
- React Best Practices
- React Native Skills
- Web Design Guidelines

Then we can choose with which model, e.g. Claude Code, Copilot etc.

It then creates a couple folders and files in the places we decided to go in, e.g. .github/skills or .claude/skills.

We can then hide these in .gitignore.
