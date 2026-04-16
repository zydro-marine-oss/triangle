# Triangle (Zydro Fork)

Fork of [drufat/triangle](https://github.com/drufat/triangle) with pre-built Linux wheels for x86_64 and aarch64.

The upstream package has not published a PyPI release since 2022, and the stale Cython-generated C code fails to compile on aarch64. The upstream `main` branch has the fix (regenerated with Cython 3.0.11) but no release was cut. This fork builds and publishes wheels from that fixed code.

## Usage

In `requirements.txt`:

```
triangle==20250106
```

In `Dockerfile`:

```dockerfile
pip install \
  --find-links https://github.com/zydro-marine-oss/triangle/releases/expanded_assets/latest \
  -r requirements.txt
```

## Publishing a new release

Wheels are built automatically by GitHub Actions when a tag is pushed. Tags created via the GitHub UI do not reliably trigger workflows -- use git:

```bash
git tag v0.0.2
git push origin v0.0.2
```

This builds cp310 Linux wheels (x86_64 + aarch64) and attaches them to a GitHub Release. The workflow can also be triggered manually from the Actions tab, which publishes to a `latest` rolling release.

## Upstream

[Triangle](https://www.cs.cmu.edu/~quake/triangle.html) is a python wrapper around Jonathan Richard Shewchuk's two-dimensional quality mesh generator and delaunay triangulator library. This implementation utilizes [Cython](https://cython.org) to wrap the C API as closely as possible. Upstream source is on [GitHub](https://github.com/drufat/triangle).
