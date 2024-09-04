## LeetSyncLite GitHub Action v1.0.0 Release

### Overview

We are thrilled to announce the release of LeetSyncLite GitHub Action v1.0! This action is designed to simplify the process of syncing your LeetCode submissions directly to your GitHub repository, making it easier than ever to track and share your coding progress.

### Key Features

- **Seamless Integration:** Automatically sync your LeetCode solutions to your GitHub repository with minimal setup.

- **Lightweight and Fast:** Optimized for speed and efficiency, ensuring your LeetCode progress is always up-to-date without any unnecessary delays.

- **Flexible Configuration:** Customize how your solutions are organized and synced in your repository, tailored to your needs.

- **Secure Authentication:**  Safeguard your credentials with secure environment variables for both GitHub and LeetCode.


### Setup
1. Retrieve LeetCode cookies

   - Login to LeetCode
   - Open `Web Developer Tools`
   - Find `https://leetcode.com` from `Storage > Cookies`
   - Copy values for cookies `LEETCODE_SESSION` and `csrftoken`

2. Create a GitHub repository for LeetCode synchronization

3. Create [GitHub Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets) for LeetCode API access

   - Open `Settings > Secrets and variables > Actions` from the repository
   - Click `New repository secret`
   - Create a new secret `LEETCODE_SESSION` using `LEETCODE_SESSION` cookie value
   - Create a new secret `LEETCODE_CSRF_TOKEN` using `csrftoken` cookie value

4. Give workflows write permissions in the repository for git pushes

   - Open `Settings > Actions > General` from the repository
   - Select `Read and write permissions` from `Workflow permissions` and save

5. Create [GithHub Action](https://docs.github.com/en/actions/quickstart)

   - Create a workflow directory `.github/workflows/`
   - Create a workflow file, e.g., `leetsynclite.yml`
   - Copy the following YAML contents into the `leetsynclite.yml` file:

     ```yml
     name: LeetSyncLite
     on: workflow_dispatch
     jobs:
       build:
         runs-on: ubuntu-latest
         steps:
           - name: Run LeetSyncLite
             uses: xxiamdsk/LeetSyncLite@v1
             with:
               GITHUB_TOKEN: ${{ github.token }}
               LEETCODE_SESSION: ${{ secrets.LEETCODE_SESSION }}
               LEETCODE_CSRF_TOKEN: ${{ secrets.LEETCODE_CSRF_TOKEN }}
     ```

6. Trigger GitHub action

   - Open `Actions > LeetCode Synchronizer` from the repository
   - Click `Run workflow > Run workflow`

## Inputs

- `GITHUB_TOKEN` - **required**. GitHub token used in pushing submissions to the repository
- `LEETCODE_SESSION` - **required**. LeetCode session used in accessing LeetCode API
- `LEETCODE_CSRF_TOKEN` - **required**. LeetCode CSRF token used in accessing LeetCode API
