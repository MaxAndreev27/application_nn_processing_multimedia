# Contributing

Contributions such as bug reports, documentation improvements, and focused
code changes are welcome.

## Before opening an issue

- Search existing issues to avoid duplicates.
- Include the affected notebook/project and the steps needed to reproduce the
  problem.
- Include relevant error output, Python version, operating system, and whether
  the photo or webcam environment is in use.
- Do not attach private images or personal data. Use images you have permission
  to share.

## Changes

1. Create a branch for your change.
2. Keep changes focused and preserve the separation between the photo and video
   environments. They intentionally use different OpenCV distributions.
3. Update documentation and requirements when behavior or setup changes.
4. Run the affected notebook cells or an equivalent focused check. Do not
   require a webcam for checks that can be performed on a sample frame.
5. Avoid committing virtual environments, downloaded model weights, generated
   output, or private data.
6. Open a pull request describing the change, how it was checked, and any
   limitations.

By submitting a contribution, you confirm that you have the right to submit
it under the repository's MIT License. This does not relicense third-party
components or example images.
