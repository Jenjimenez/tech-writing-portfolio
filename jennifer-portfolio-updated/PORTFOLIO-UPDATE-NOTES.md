# Portfolio update notes

## What changed

This is a presentation update to the uploaded `tech-writing-portfolio-main(1).zip`, not a technical or editorial rewrite of the writing samples.

The site retains `jekyll-theme-minimal`, with local HTML layouts and CSS that replace its default presentation. The homepage now puts writing samples before the longer About section. It displays three featured cards and two additional cards, each with a document type, description, audience, demonstrated writing skills, and a direct reading link.

Featured order:

1. Author onboarding and messaging playbook.
2. Getting started with in-app guidance.
3. End user schema API reference.

The SOP and knowledge-base article follow under More writing samples. This ordering is a presentation recommendation, not a certification that the samples are ready to publish.

The stronger introduction from the original README is now reflected on the public homepage. The knowledge-base card uses the actual `Knowledge_Base_Articles` directory. The README email link now uses `mailto:`. The missing resume link is hidden until an actual resume path is supplied.

Each sample has a consistent reading layout with audience and skills context, a link back to the homepage, and links to other writing samples. All five original sample bodies are unchanged. Only a YAML front-matter block was added to each sample file. No authorship claims, metrics, measured outcomes, or new sample content were invented.

## Apply the update

1. Back up your current repository or use a separate branch to review the design.
2. Unzip this archive and copy the **contents** of `jennifer-portfolio-updated` into the root of the repository. Do not add the enclosing directory as another folder inside the repository. Replace the matching existing files and include the new `_layouts`, `_includes`, `_data`, and `assets` folders. Preserve any repository files that were not in the supplied ZIP.
3. Check `baseurl` in `_config.yml`. The supplied value is `/tech-writing-portfolio`, based on the archive name. For a project repository with another name, use `/YOUR-REPOSITORY-NAME`. For a custom domain or a `USERNAME.github.io` repository, use `""`. The optional `url` setting can hold your site's origin, with no repository path or trailing slash.
4. Complete the content and permission checks below **before** publishing. An update to a configured publishing branch can publish automatically.
5. For a standard GitHub Pages branch build, confirm the publishing source is the branch containing these files and `/ (root)` under Settings > Pages. Keep your existing workflow if you already use GitHub Actions, and check that it runs Jekyll against the same source directory.
6. After deployment, check the homepage, all five sample links, stylesheets, contact links, keyboard navigation, and mobile layout on the actual hosted site. Inspect the GitHub Pages build result for errors.

Updating only `_config.yml` will not produce the new layout. The complete set of changed files is required.

## Maintain the portfolio

| File | Purpose |
| --- | --- |
| `_config.yml` | Name, professional title, contact details, base path, and optional resume link. |
| `index.md` | Public homepage content and sample sections. |
| `_data/samples.yml` | Sample titles, descriptions, audiences, skills, display order, and featured status. |
| `_includes/sample-card.html` | Reusable homepage card markup. |
| `_layouts/default.html` | Shared page structure, navigation, metadata, and footer. |
| `_layouts/sample.html` | Shared sample-page context and return navigation. |
| `assets/css/portfolio.css` | Visual presentation and responsive styling. |
| Existing sample Markdown files | The actual writing samples. |

To feature a different sample, edit its `featured` value and reorder the entries in `_data/samples.yml`. Three featured samples is the intended desktop layout. To add a new sample, create its Markdown file with `layout: sample` and a unique `sample_id`, then add a matching entry in the YAML data file.

A blank `contribution` field is provided for every sample. Add a verified sentence about your actual role, such as writing, editing, restructuring, or validation. A filled field will appear as **My contribution** on that sample page. Do not imply sole authorship of collaborative work.

To add a resume, upload the actual PDF to a path such as `assets/Jennifer_Botia_Resume.pdf`, then set `resume_path: "/assets/Jennifer_Botia_Resume.pdf"` in `_config.yml`. The navigation and contact section will display resume links once that value is populated. No resume was included in the original archive.

## Content checks before publishing

The redesign deliberately preserves the existing sample text. These source issues remain:

| Sample | Required follow-up |
| --- | --- |
| API reference | Replace the `(link)` placeholder for the API integration-key instructions. Reconcile the table of contents with the body: several entries point to missing or differently named sections. Verify the endpoints, required parameters, and examples against an approved source before presenting the sample as technically validated. |
| Web user guide | Replace `(link)` and `(#)` placeholders. Review product references written as `x` and associated `x.com` links. Verify the referenced resources, and label any anonymization clearly. |
| Knowledge-base article | Replace the tutorial `(link)` placeholder and review the `x` product references and associated external links. |
| SOP | Add the referenced `image1.png` screenshot, or deliberately remove the image reference. The screenshot was not supplied. |
| Author onboarding playbook | Confirm public-sharing permission, remove internal-only or confidential details as needed, and describe your actual contribution. This update did not redact or approve the document for publication. |
| All samples | Check heading consistency, terminology, accuracy, proofreading, attribution, and public-sharing permission. Explain whether each piece is original, collaborative, edited, adapted, or anonymized. |

Some placeholders in reusable message templates are intentional and should remain. These are different from unfinished navigation links such as `(link)`.

## Validation performed and limitations

- Confirmed that all five sample bodies are unchanged after removing the newly added YAML front matter.
- Parsed the YAML configuration and sample metadata successfully.
- Rendered the homepage and all five sample pages using a limited Liquid-compatible preview renderer and Mistune Markdown, then inspected the HTML/CSS in Chromium. This was **not** a Jekyll build; Markdown rendering and anchor details may differ from GitHub Pages.
- Confirmed that all five homepage sample URLs map to existing generated local preview files, and checked the new navigation targets. This is not an HTTP availability test of the live site.
- Checked the homepage at widths of 320, 390, 768, and 1440 pixels and each sample at 390 pixels, with no horizontal viewport overflow in those checks.
- Visually inspected desktop and mobile homepage previews and a sample-page preview. Confirmed that the skip-to-content link is the first keyboard tab target.
- Flagged the existing placeholder, missing-resource, and table-of-contents issues above. External sample URLs were not verified.

The actual Jekyll build and GitHub Pages deployment were not run. Jekyll and its gems were unavailable in the working environment, and the package host could not be resolved. No changes were made to the live site or GitHub repository. Review the hosted build before relying on this version for applications.

## Reference documentation

- Minimal theme customization: https://github.com/pages-themes/minimal
- Jekyll layouts: https://jekyllrb.com/docs/layouts/
- Jekyll front matter: https://jekyllrb.com/docs/front-matter/
- Jekyll relative URL filter: https://jekyllrb.com/docs/liquid/filters/
- GitHub Pages publishing source: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
