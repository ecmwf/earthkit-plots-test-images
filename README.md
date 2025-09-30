# earthkit-plots-test-images

This repository contains baseline images for the visual regression testing of [earthkit-plots](https://github.com/ecmwf/earthkit-plots). These images serve as reference points to ensure that plot generation remains consistent across code changes and releases.

> \[!IMPORTANT\]
> This repository is automatically cloned and used by the earthkit-plots testing suite. **Most users don't need to interact with this repository directly**.

## Purpose

The baseline images in this repository are used by the earthkit-plots CI pipeline to perform:

- **Visual regression testing**: Compare newly generated plots against established baselines
- **Quality assurance**: Detect unintended changes in plot appearance
- **Release validation**: Ensure visual consistency across earthkit-plots versions

## How It Works

### Integration with earthkit-plots

1. **Automatic Setup**: When running image tests in earthkit-plots, this repository is automatically cloned to `tests/.earthkit-plots-test-images/`
2. **Test Execution**: The pytest-mpl plugin compares newly generated images against the baselines stored here
3. **CI Pipeline**: The earthkit-plots CI automatically uses these baselines for visual regression testing

### Test Commands in earthkit-plots

From the earthkit-plots repository root:

```bash
# Run image tests (compares against baselines)
make image-tests

# Generate new baseline images
make generate-test-images

# Set up the test images repository locally
make setup-test-images
```

## Updating Baseline Images

When plot generation changes in earthkit-plots require updated baselines, follow this process:

### 1. Generate New Images

From the earthkit-plots repository:

```bash
# Generate updated baseline images
make generate-test-images
```

This creates new images in `tests/.earthkit-plots-test-images/baseline-images/`

### 2. Review Changes

Carefully review the generated images to ensure they represent intended changes:

```bash
cd tests/.earthkit-plots-test-images
git status
git diff --name-only
```

### 3. Create Pull Request

Create a new branch and push the changes:

```bash
cd tests/.earthkit-plots-test-images
git checkout -b update-baselines-YYYY-MM-DD
git add .
git commit -m "Update baseline images for [describe changes]"
git push origin update-baselines-YYYY-MM-DD
```

### 4. Submit PR

Create a pull request against this repository with:
- **Clear description** of what changed and why
- **Link to the corresponding earthkit-plots PR** that necessitates these changes
- **Visual comparison** if significant changes are involved

## Best Practices

### For Maintainers

- **Coordinate releases**: Baseline updates should be merged alongside corresponding earthkit-plots changes
- **Review carefully**: Visual changes should be intentional and documented
- **Test locally**: Always run `make image-tests` in earthkit-plots before merging baseline updates

### For Contributors

- **Minimal changes**: Only update baselines when necessary
- **Clear commits**: Use descriptive commit messages explaining the reason for baseline changes
- **Link PRs**: Always reference the related earthkit-plots issue/PR

## Technical Details

### Image Format
- **Format**: PNG
- **Comparison**: Pixel-by-pixel using pytest-mpl
- **Tolerance**: Configurable in earthkit-plots test configuration

### Dependencies
- Used automatically by earthkit-plots testing infrastructure
- No direct dependencies or setup required in this repository
- Images are generated using matplotlib and earthkit-plots

## Troubleshooting

### Common Issues

**Images not found during tests**:
```bash
# Ensure the repository is properly cloned
make setup-test-images
```

**Local baseline differs from remote**:
```bash
# Check for uncommitted changes
make check-test-images-sync
```

**Test failures after baseline updates**:
- Ensure both earthkit-plots and baseline changes are compatible
- Verify that the baseline images correspond to the correct earthkit-plots version

## Related Repositories

- [earthkit-plots](https://github.com/ecmwf/earthkit-plots) - Main plotting library
- [earthkit](https://github.com/ecmwf/earthkit) - Parent ecosystem

## License

```
Copyright 2023, European Centre for Medium Range Weather Forecasts.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

In applying this licence, ECMWF does not waive the privileges and immunities
granted to it by virtue of its status as an intergovernmental organisation
nor does it submit to any jurisdiction.
```
