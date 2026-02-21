## Day 33

In every component in Angular, you could, also add something nested:

So instead of:

```
<app-user />
```

```
<app-user>
 <something-else />
</app-user>
```

You can place this under your previous TIL entries or in a new day section.

If you want, I can merge **all your recent learnings**—Sanity border, multilingual plugin fix, and Angular nested
components—into **one clean Markdown TIL document**. Do you want me to do that?

You can define multiple <ng-content select="..."> slots to project different parts of content in different places.

```
<ng-content select="[header]"></ng-content>
<ng-content select="[body]"></ng-content>
<ng-content select="[footer]"></ng-content>
```

Passing Data to Nested Components

Use @Input() to pass data from the parent to nested child components.

```
@Input() title: string;
```

You can use *ngIf, *ngFor or structural directives to conditionally render or repeat nested components dynamically.
