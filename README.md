# Prashant C Chaturvedi - Personal Website & CV

This repository contains the source code for my personal website and digital Curriculum Vitae (CV). The site is statically generated and hosted on GitHub Pages.

## 🚀 Live Site
[https://pccofvns.github.io](https://pccofvns.github.io)

## 🛠 Tech Stack

The site is built using modern, lightweight static web technologies:

*   **Static Site Generator:** [Jekyll 4.4](https://jekyllrb.com/)
*   **CSS Framework:** [Bootstrap 5.3](https://getbootstrap.com/)
*   **Icons:** [Font Awesome 6.7](https://fontawesome.com/)
*   **Styling:** Sass / SCSS natively compiled by Jekyll
*   **CI/CD:** GitHub Actions

## 📂 Project Structure

Here are the most important directories and files in this project:

*   **`_data/cv.yml`**: The central configuration file that drives the content of the CV (experiences, skills, contact info, etc.). **Update this file to change resume content.**
*   **`_includes/`**: Reusable HTML partials. The `cv/` subdirectory contains the individual sections of the resume (e.g., `experiences.html`, `skills.html`).
*   **`_layouts/`**: The main page wrappers.
*   **`_sass/` & `assets/css/`**: The stylesheets. The theme configuration is in `assets/css/cv.scss`, which imports `skins/ceramic`.
*   **`cv.html` & `index.html`**: The main entry points for the CV page and the homepage.

## 💻 Local Development Setup

To run this site locally on your machine, follow these instructions.

### Prerequisites
You will need Ruby and Bundler installed. If you are on a Mac, it is highly recommended to use a Ruby version manager like `chruby`, `rbenv`, or `rvm` instead of the system Ruby.

```bash
# Example setup using Homebrew & chruby (macOS)
brew install chruby ruby-install
ruby-install ruby-4.0.2

# Add to your ~/.zshrc or ~/.bash_profile
echo "source $(brew --prefix)/opt/chruby/share/chruby/chruby.sh" >> ~/.zshrc
echo "source $(brew --prefix)/opt/chruby/share/chruby/auto.sh" >> ~/.zshrc
echo "chruby ruby-4.0.2" >> ~/.zshrc
source ~/.zshrc
```

### Installation

1.  Clone the repository:
    ```bash
    git clone https://github.com/pccofvns/pccofvns.github.io.git
    cd pccofvns.github.io
    ```
2.  Install dependencies:
    ```bash
    bundle install
    ```

### Running the Site
Start the local Jekyll development server:
```bash
bundle exec jekyll serve --livereload
```
The site will be available at `http://localhost:4000`. The `--livereload` flag automatically refreshes your browser when you make changes to files.

## 🚢 Deployment

This site is automatically deployed to GitHub Pages via **GitHub Actions**. 
Any push to the `master` branch triggers the deployment workflow defined in `.github/workflows/jekyll-gh-pages.yml`. The workflow builds the Jekyll site and publishes the artifact to GitHub Pages.

## 📝 Updating the Content

- **To update CV details:** Edit `_data/cv.yml`. The template will automatically render the new data.
- **To change the theme color:** Open `assets/css/cv.scss` and change `@import "skins/ceramic";` to another skin file located in `_sass/skins/`.
- **To write a blog post:** Add a new Markdown file in the `_posts/` directory following the `YYYY-MM-DD-title.md` naming convention.
