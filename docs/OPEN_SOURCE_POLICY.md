# CoBeing publication policy / 开源与公开发布规范

**Default intent:** open mature, independently useful outcomes. **Not:** expose all unfinished engineering or third-party-specific experiments as they happen.

## Repository roles

- **Public:** CoBeing's stable vision, open documentation, runnable released code, clean protocol/schema references and verified reusable adapters.
- **Private incubation:** incomplete UI, memory, device/network and service integrations; internal design alternatives and experiments.
- **Private integration lab:** third-party compatibility explorations, temporary fixtures, provider-specific investigations and pre-release adapters.

The initial working repositories may be private. A mature component should be published in a **separate clean public repository** rather than simply changing an old experimental repository from private to public. GitHub visibility changes can expose history and Actions logs.

## Small release gate — only four checks

1. **Works:** One useful end-to-end user scenario works, with essential targeted tests; unfinished features are honestly labeled.
2. **Safe to disclose:** No personal chats, credentials, secrets, private endpoints, customer/partner information or sensitive logs in source, commits, examples and artifacts.
3. **Rights and boundaries:** Authors have permission to publish; third-party code, SDK, data, screenshots, marks and protocol material are reviewed for license and contractual restrictions. Link to upstream when possible rather than copying it.
4. **Usable:** README explains purpose, setup, supported scope, known limits, license and how to report a real problem.

Avoid giant pre-release checklists. Publish a small working slice rather than a speculative platform skeleton. Unstable APIs can remain private until their minimum contract is dependable.

## Third-party adapters

- Prefer official/open interfaces and user-supplied, explicitly authorized credentials.
- Keep third-party implementations separate from the CoBeing Basic core.
- Publish only sanitized, independently licensed code and synthetic examples.
- Do not commit token files, downloaded proprietary SDK bundles, real messages, sensitive endpoint inventories or access-bypass scripts, **even to private repositories**.
- Disclosure of an adapter does not claim provider affiliation or formal support.

This policy governs publication scope; it is not a restriction on appropriate private development or legitimate interoperability research.
