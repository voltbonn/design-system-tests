# Visual regression testing for Volts design system

The only purpose of this repository is to execute visual regression tests and generate reports for Volts design system. This project will be used in the build pipeline of the Volts design system repository. The reports are very helpful in checking for visual changes which may have been unintended.

## How to use

### Clone the repository

This repository uses (git-lfs)[https://git-lfs.github.com/]. As we are storing lots of binary data (the images) in this project, the size of the project would explode with more and more changes. So we are storing the images using git-lfs. Make sure you have installed it (as mentioned in the documentation)[https://github.com/git-lfs/git-lfs?utm_source=gitlfs_site&utm_medium=source_link&utm_campaign=gitlfs]. After downloading and installing the binaries a `git lfs install` should do the job.

### Run the tests

First of all you have to start storybook in the design system repository. Make sure it runs on port 6006.
Then you can run the tests:

```bash
npm run test
```

This will capture screenshots of the stories in storybook, test the differences with the pictures in the folder 'reference' and generate a report.html file you can open in a browser to see the results and diffs.

## Only for project maintainers

To accept the changes run

```bash
npm run accept
```

This will rerun the test and copy the images from the folder 'current' into 'reference'.

## How does it work?

We are using [storycap](https://github.com/reg-viz/storycap) to take the screenshots. Storycap will use a headless chromium or puppeteer to create the screenshots.

_Note that_ storycap is also a dependency of the design system itself. So it's possible to configure the screenshot options in the original repo. By executing storycap in this project the configs will be used to take the screenshots.

After the screenshots are saved in the folder 'current' we will run [_reg-cli_](https://github.com/reg-viz/reg-cli). This tool compares two images, calculates a diff and generates the report. The report supports different visual methods to spot changes for each image. It also shows which images are new, were deleted, have failed (because they're different) or passed (because they're visually the same).

## Who is this project for?

Everybody can use this project to spot changes they made in Volts design system. It is especially useful to spot sideeffect that weren't made to happen. Don't worry if the test fails after you made changes (even small ones) - that's the whole purpose of this project.

Don't update the reference images by yourself. Only the project maintainers will do this. Otherwise we would not be able to keep track of changes and something (big) messed up might go unnoticed into the next version of the design system.
