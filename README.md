# cpr-documentation

## Links to the deployed website:

- [_production_ branch](https://docs.clearpathrobotics.com)
- [_development_ branch](https://development.dfy90wyu8dics.amplifyapp.com/)

## Tools used:

1.  [Node.js](https://nodejs.org/en/)
2.  [Docusaurus](https://docusaurus.io/) _by Facebook / Meta_
3.  [GitHub](https://github.com/)
4.  [AWS Amplify](https://aws.amazon.com/amplify/)

## Steps to run this on your computer locally:

1.  System dependencies, common to most web development
    1.  VS code, or similar editor
        - Extension: _Git Lens_
        - Extension: _Prettier_
        - Extension: _MDX_
    2.  Terminal configured to work with this GitHub repository
    3.  Node.js is installed
2.  Clone this repository,

        git clone https://github.com/clearpathrobotics/cpr-documentation.git

3.  Open the folder
4.  In a terminal, navigate to the root of the project folder and run `npm install`
5.  Start the local server by running `npm run start`
6.  A new tab should open in your prefered web browser once the site is running.
    Your terminal session should show the port the webpage is running on.
    The default address is http://localhost:3000/ but this may change if you are already using that port for another site.
7.  If you want to test something on a mobile screensize; you can do this within your desktop's Chrome browser.
    When the site is running locally; enter Chrome's developer tools by selecting: _3 dots in the top right_ → _More tools_ → _Developer tools_.
    You can then select the _Device Toolbar_ button, and change the screensize, as shown in the two images below.
    We are designing to a smallest screen width of 320 px.

    <img src="/static/img/readme_images/readme_chrome_developer_1.png" width="800"/>

    <br />

    <img src="/static/img/readme_images/readme_chrome_developer_2.png" width="800"/>

## Workflow for making updates:

1.  Clone or fork this repository,

        git clone https://github.com/clearpathrobotics/cpr-documentation.git`

2.  Create a branch from development. with a name indicating the purpose, such as _feature_xxxxxx_
3.  Make changes to the relevant files
4.  Test using your local server, using the steps mentioned [Steps to run this on your computer locally](##-steps-to-run-this-on-your-computer-locally)
5.  When ready, enter `ctrl-c` in your terminal to stop the server. Then run `npm run build` to test that the site builds corretly.
6.  Resolve any errors that the terminal reports, and rerun the command `npm run build`.
7.  Finally, check that your updates adhere to our code formatting standard, by running the command `npm run format-check`.
    The terminal will either report:
    - _All matched files use Prettier code style!_
    - _Code style issues found in the above file(s). Forgot to run Prettier?_
      You can fix the errors by running the command `npm run format-write`.
      This format all the files in the repository, and save them automatically.
      - Refer to the _package.json_ to understand what this script calls.
      - Refer to the _.prettierrc.json_ to understand the rules Prettier is using when checking files.
      - Alternativaly, you can format a single file by running `npx prettier --write <FILE PATH>`, such as `npx prettier --write README.md`
8.  You will need to confirm that `npm run format-write` code formatting did not make any functionality changes to your _.mdx_ documentation.
    You may see files that claim to be updated in Source Control, but don't have any visible changes.
    You should run these commands in your terminal to prevent Git from noting these types of changes:

        git config --global core.filemode false
        git config --global core.autocrlf false

9.  When ready, publish your branch on GitHub, and submit a Pull Request to merge your changes into the _development_ branch.
    Pull Requests to the _production_ branch will not merged.
    Also note that this GitHub repository has branch protection rules, that prevent you from committing directly to _production_ and _development_.

    <img src="/static/img/readme_images/readme_github_1.png" width="467"/>

10. The administrators of this documentation will review the website for any functional issues,
    and will periodically merge the latest commits in the _development_ branch into the _production_ branch.

## Workflow for publishing OutdoorNav User Manual updates

The OutdoorNav User Manual is a "versioned" document, which means that a snapshot of the content is
made to align with a release. This allows users to access version-specific copies of the
documentation.

### Development Phase

During the development phase, follow steps 1-10 of the workflow above. Note that the updates will not affect
the default view of the user manual, only the "next" version of the manual
(eg. http://docs.clearpathrobotics.com/docs_outdoornav_user_manual/next/index).

### Release Phase

When it is time to publish a numbered release of the user manual:

1.  Create a branch from _development_ with a name indicating the purpose, such as _release_xxxxxx_
2.  Run the versioning command, where _new_version_ is aligned with the corresponding software release:

        npm run docusaurus docs:version:outdoornav_user_manual <new_version>

3.  Update /docs/software/navigation_packages.mdx to:
    - Update the version number for the "Latest".
    - Add an entry for the previous release.
4.  Update /static/versions.js to update the outdoornav version to match the GitHub tag.
5.  Build and test the changes (see steps 4-8 from the standard workflow above).
6.  When ready, publish your branch on GitHub, and submit a Pull Request to merge your changes into the _development_ branch.
    Be sure to include the updates to the following:
    - outdoornav_user_manual_versioned_docs/
    - outdoornav_user_manual_versioned_sidebars/
    - outdoornav_user_manual_versions.json

## Workflow for publishing OutdoorNav User Manual updates

Follow the steps for the OutdoorNav User Manual workflow above, replacing
**outdoornav** with **indoornav**.

## How should I write pages?

1.  Refer to [Markdown's guide](https://www.markdownguide.org/basic-syntax/) for syntax
2.  Refer to [Docusaurus's guide](https://docusaurus.io/docs/next/markdown-features) for supported Markdown features
3.  For advanced users, refer to [Markdown MDX](https://mdxjs.com/) for adding React Components to a Markdown file
4.  for advanced users, you may create React pages using _.js_ or _.ts_ file types

## How should I name files?

All files should use lowercase letters for their names and file extensions.
Our website's server is case sensitive, so it requires files case to match how it is called in your Markdown files.
Your Windows build commands may not catch these issues since Windows is not case sensitive.
Using lowercase letters minimizes the number of build issues.

- Good: `controller_1.png`
- Bad: `Controller_1.png`
- Bad: `controller_1.PNG`

Downloadable assets like PDFs should say _clearpath_robotics_ at the start of the name.
This helps User's know where they downloaded the file from later, as the asset is saved to their _Downloads_ folder.

## Where should I place files?

1.  Markdown page

        /docs

2.  Markdown component, like a section to be reused in multiple pages

        /components

3.  Images

        /static/img

4.  PDFs and similar customer facing files

        /static/assets

## How does the deployed website get updated?

We have this site deployed on _AWS Amplify_.
Their server is monitoring the _production_ and _development_ branches of this repository.
When AWS sees a new commit on either branch, it will rebuild the site.
The image below shows the _development_ branch rebuilding after the GitHub branch was updated by a Pull Request.

<img src="/static/img/readme_images/readme_aws_1.png" width="800"/>

This example took 2 minutes and 14 seconds to deploy.
If your _feature_ branch change is large, we can deploy it as a temporary site on AWS to confirm that it builds before submitting a Pull Request into Development.
The downsides of deploying more branches are:

- Possible time lost, though this may save time by preventing build errors on the _production_ branch
- A small cost to AWS for using their Server.
  At the time of writing (May 2022), [AWS charges](https://aws.amazon.com/amplify/pricing/) $0.01 USD per build minute.

## Structure for pages

You can find templates in the directory _/static/reference_pages_

## Equations

You can add equations using [KaTex syntax](https://katex.org/docs/supported.html).
The packages have are installed in the _package.json_ and imported into the project in _docusaurus.config.js_.
You simply need to add your equations to your Markdown file, keeping all the elements between opening an closing tags _$_.

$$
\omega=\cfrac{v_{r}-v_{l}}{w}
$$

You can test equation syntax using [this tool](https://katex.org/) from KaTex.

## Image formatting

We want images to convey information.
The best way to do this is to have a consistent method notating images, and removing unnecessary content.
The list below are not strict rules, but are considered good practice to keep images throughout the site looking consistent,

1.  Highlight colours should be:
    1.  Primary
        - #BB0000
        - RGB (187, 0, 0)
    2.  Secondary
        - #00C7A6
        - RGB (0, 199, 166)
    3.  Tertiary
        - #4E7FFF
        - RGB (78, 127, 255)
2.  Remove background colours when possible.
    This helps Users that have set the site to Dark Mode.
    Refer to _SolidWorks image exports_ for the process of creating these images.
3.  Avoid embedding text in images.
    This prevents Users from translating the webpage.
    Consider using arrows and circles to notate images, with the text included in your Markdown file.

    Note: icons, logos, and symbols that are part of the physical product are exempt from this suggestion.

## SolidWorks image exports

1.  Open your assembly in SolidWorks.
    Orient the model to the view you want to capture.
    Click _File_ → _Save-As_.

    <img src="/static/img/readme_images/readme_solidworks_image_1.png" width="800"/>

2.  Select _.png_ as the file type.
    Then click the _Options_ button.

    <img src="/static/img/readme_images/readme_solidworks_image_2.png" width="800"/>

3.  Make sure the _Remove background_ box has a check mark.
    Click the _Print capture_ box, so you can manually choose the image's width and height.

    <img src="/static/img/readme_images/readme_solidworks_image_3.png" width="800"/>

4.  In the same window as Step 3; scroll down to the bottom.
    Change the _Width_ and _Height_ fields to adjust the bounding box around the SolidWorks model.
    300 mm tall should be a good balance between image resolution and file size.

    Finally, select _OK_, and _Save_

    <img src="/static/img/readme_images/readme_solidworks_image_4.png" width="800"/>
