# LiveAPI Documentation

Welcome to the unofficial **LiveAPI Documentation** repository. This documentation site is built with [Hugo](https://gohugo.io/), utilizing the [Lotus Docs](https://github.com/colinwilson/lotusdocs) theme for a streamlined, intuitive documentation experience that supports multilingual content.

## Getting Started

Follow these instructions to set up a local development environment and contribute to the LiveAPI Documentation.

### Prerequisites

- [Hugo](https://gohugo.io/overview/installing/) must be installed on your system. For installation instructions, see the [official Hugo documentation](https://gohugo.io/overview/installing/).

### Installation

1. **Clone the Repository:**

   ```bash
   git clone --depth 1 https://github.com/YourGitHubUsername/apex-liveapi-documentation liveapi-documentation
   cd liveapi-documentation
   ```

   Replace `YourGitHubUsername` with the actual username or organization name under which the repository is hosted.

2. **Add the Custom Lotus Submodule:**

   ```bash
   git submodule add https://github.com/zeejayym/lotusdocs.git themes/lotusdocs
   git submodule update --init --recursive
   ```
3. **Run Hugo Server:**

   ```bash
   hugo server
   ```

   This command starts a local web server. Open `http://localhost:1313` in your browser to view the documentation.

## Contributing

We welcome contributions to the LiveAPI Documentation! To contribute:

1. **Fork the Repository:** Start by forking the LiveAPI Documentation repository to your GitHub account.

2. **Clone Your Fork:**

   ```bash
   git clone https://github.com/YourUsername/apex-liveapi-documentation
   cd liveapi-documentation
   ```
3. **Add the Custom Lotus Submodule:**

   ```bash
   git submodule add https://github.com/zeejayym/lotusdocs.git themes/lotusdocs
   git submodule update --init --recursive
   ```

4. **Create a New Branch:**

   ```bash
   git checkout -b your-branch-name
   ```

   Use a descriptive name for your branch (`your-branch-name`) based on the changes you intend to make.

5. **Make Your Changes:** Add or edit content as needed.

6. **Commit Your Changes:**
   Please use the [commitizen](https://github.com/commitizen/cz-cli) if you're unfamiliar with commiting!

   ```bash
   git add .
   git commit -m "feat: A descriptive message about your changes"
   ```

1. **Push to Your Fork:**

   ```bash
   git push origin your-branch-name
   ```

2. **Open a Pull Request:** Navigate to the original `liveapi-documentation` repository you forked. You'll see a prompt to open a pull request. Fill in the details, explaining the changes you've made.

3.  **Await Review:** Your pull request will be reviewed by the maintainers, and if everything is in order, it will be merged into the main documentation.

## Acknowledgments

- **Hugo**: For powering our documentation site. More about Hugo can be found [here](https://gohugo.io/).
- **Lotus Docs Theme**: For the beautiful theme design. Thanks to [Colin Wilson](https://github.com/colinwilson) and all contributors. Visit the theme [here](https://github.com/colinwilson/lotusdocs).

---
