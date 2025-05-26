#  Issue: Problem Adding Image to README.md

## Problem
Tried to add an image to `README.md` using HTML (`<img src="..." />`) — did not work, the image wasn't displayed.

## Solution
The working way is to upload the image via the GitHub UI and use a Markdown link.

##  STEPS 

1. Open [GitHub.com](https://github.com) in your web browser.
2. Navigate to your target repository.
3. Click **"Add file"** → **"Upload files"**.
4. Drag and drop your image file into the upload area.
5. Click **"Commit changes"**.
6. Find and open the uploaded image file in the repo.
7. Right-click the image and select **"Copy image link"**.
8. Open your `README.md` file and click the pencil (edit) icon.
9. Add the following Markdown code :
   ```markdown
   ![Alt text](image_url)

