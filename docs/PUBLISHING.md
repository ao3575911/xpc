# Publishing `xpc` to PyPI

Trusted Publishing only (OIDC). No long-lived API tokens.

## Version

- Package version: `pyproject.toml` → `[project].version` and `src/xpc/__init__.py` → `__version__`
- GitHub release tag must match (`v0.2.0` ↔ `0.2.0`)

## One-time: Trusted Publishers

1. Create empty GitHub Environments: `testpypi`, `pypi` (done in repo settings).
2. [TestPyPI](https://test.pypi.org/manage/account/publishing/) → Pending publisher for project **`xpc`**:
   - Owner: `ao3575911`
   - Repository: `xpc`
   - Workflow: `publish.yml`
   - Environment: `testpypi`
3. [PyPI](https://pypi.org/manage/account/publishing/) → same with Environment: `pypi`

## Flows

| Trigger | Target |
|---------|--------|
| `workflow_dispatch` → `testpypi` | TestPyPI |
| `workflow_dispatch` → `pypi` | PyPI |
| GitHub Release `published` | PyPI |

```bash
gh workflow run publish.yml -f target=testpypi --repo ao3575911/xpc
# after TestPyPI green:
gh release create v0.2.0 --generate-notes --repo ao3575911/xpc
# or: gh workflow run publish.yml -f target=pypi
```

## Verify

```bash
pip install -i https://test.pypi.org/simple/ --extra-index-url https://pypi.org/simple/ xpc==0.2.0
# prod:
pip install xpc==0.2.0
xpc --version
xpc validate --help
```
