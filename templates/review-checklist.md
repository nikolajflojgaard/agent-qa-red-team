# Review Checklist

## Code QA

- [ ] Does the change solve the requested behavior?
- [ ] Are there edge cases, error paths, or state transitions missing?
- [ ] Could the change break existing contracts?
- [ ] Are tests targeted to the risk?

## Docs QA

- [ ] Are links, commands, diagrams, and examples accurate?
- [ ] Are generated docs checked for drift?
- [ ] Are assumptions marked instead of stated as fact?

## Security / Privacy

- [ ] Are secrets, tokens, keys, or private data exposed?
- [ ] Are external actions approved?
- [ ] Are auth, permissions, and trust boundaries clear?

## Validation QA

- [ ] Were the strongest practical checks run?
- [ ] Did any command fail?
- [ ] Is CI/deploy status verified when relevant?
- [ ] Are skipped checks explicitly reported?

## Reasoning Red Team

- [ ] Are claims backed by evidence?
- [ ] Is the scope honest?
- [ ] Are time-sensitive facts verified?
- [ ] Is the final report overclaiming?
