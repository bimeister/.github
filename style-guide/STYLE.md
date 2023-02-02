# Style Guide — Bimeister

## General Principles

### 1. Expressiveness is more important than brevity.

> All developers know the codebase differently. Developer expertise is also different. As we strive for continuous development of our projects, it is important that the codebase remains maintainable and extensible, no matter what language it is written in. \
> For example, if we are writing Bash scripts, try to use full flags instead of shorthand ones, this will make your code readable even by people who are not particularly familiar with Bash:

```bash
rm --recursive --force ./ # instead of: rm -rf ./
```

### 2. Reusability of practices in the codebase.

> Similar tasks should be solved in the same way in different parts of the code base. Despite the fact that in programming you can reach the same result in completely different ways, in the same codebase such diversity is often just extra noise that interferes with reading and quick immersion in the code.

### 3. Agreed practices are non-negotiable.

> The code submitted for review must fully comply with all accepted standards. This does not mean that standards cannot be changed — in order to make changes to the standard, you need to start the process according to the regulations. But this means that code reviews are not the place for discussions about the quality of regulations and their applicability.

### 4. Controversial issues are resolved by codeowners voting.

> If the result of a code review is a discussion that can't be resolved by simple reasoning, Codeowners can choose a majority vote decision.

### 5. Issues that could not be resolved by voting are solely resolved by the community leader (Tech Lead / Team Lead / ...).

> The community leader has the right to make a decision alone if the participants in the discussion could not reach a consensus.

---

## Prohibited changes

1. Code that has been pointed out by a reviewer as being unreadable or unclear.
2. Code that does not comply with the design rules adopted on the project.
3. Code containing duplicates.
4. Changes containing commented code.
5. Changes that contain unreachable or non-callable code.
6. Unnecessarily deleted tests that were running.
7. Other changes pointed out by the reviewer as invalid. In the absence of a compromise, the team makes a decision by a simple majority vote.

---

## Language Rules

1. [CSS (SCSS)](./STYLE_CSS.md)
2. [TypeScript (JavaScript)](./STYLE_TS.md)
