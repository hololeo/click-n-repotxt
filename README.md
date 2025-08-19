# Click 'n' RepoTxt
A bookmarklet for rapid repo text extraction. Just click and download!

Powered by [uithub.com](https://uithub.com/) - an amazing service for GitHub repository content extraction.

<img src="https://github.com/user-attachments/assets/placeholder-icon" width="150">

**If this work has been helpful to you, you can support it for free by clicking ⭐ to star this repository!**

### Quickly Convert GitHub Repos to Downloadable Text with Bookmarklet

To quickly convert any GitHub repository to downloadable plain text format, follow these steps:

1. **Set up the bookmarklet**:
   - **Easy method**: Go to the [Bookmarklet Maker](https://caiorss.github.io/bookmarklet-maker/) and paste the code below into the tool, then drag the generated bookmarklet to your bookmarks bar.
   - **Manual method**: Copy the minified code below, create a new bookmark in your browser, and paste it into the bookmark's URL field.
     
```javascript
javascript:(function(){function convertGithubUrl(){const url=document.location.href;if(!url||!url.includes("github.com")){console.error("The current page is not a GitHub URL.");return null;}const regex=/github.com\/(.*?\/tree\/(main|master))?(.*)/;const match=url.match(regex);if(!match){console.error("Could not parse the GitHub URL.");return null;}const repoPath=match[1]||'';const remainingPath=match[3]||'';const newUrl=`https://uithub.com/${repoPath}${remainingPath}?accept=text%2Fplain&maxTokens=10000000`;return newUrl;}function initializePageHandler(){const currentUrl=document.location.href;if(currentUrl.includes("github.com")){const newFormattedUrl=convertGithubUrl();if(newFormattedUrl){console.log("Redirecting to:",newFormattedUrl);window.location.href=newFormattedUrl;}}else if(currentUrl.includes("uithub.com")){addControlButtons();}}function addControlButtons(){const pageText=document.body.innerText||document.body.textContent||'';const overlay=document.createElement('div');overlay.style.cssText=`position: fixed;top: 20px;right: 20px;z-index: 10000;background: #ffffff;border: 2px solid #333;border-radius: 8px;padding: 15px;box-shadow: 0 4px 12px rgba(0,0,0,0.3);font-family: Arial, sans-serif;`;const downloadBtn=document.createElement('button');downloadBtn.textContent='Download';downloadBtn.style.cssText=`background: #007cba;color: white;border: none;padding: 10px 20px;margin-right: 10px;border-radius: 4px;cursor: pointer;font-size: 14px;`;downloadBtn.onclick=()=>downloadText(pageText);const copyBtn=document.createElement('button');copyBtn.textContent='Copy';copyBtn.style.cssText=`background: #28a745;color: white;border: none;padding: 10px 20px;border-radius: 4px;cursor: pointer;font-size: 14px;`;copyBtn.onclick=()=>copyToClipboard(pageText,copyBtn);overlay.appendChild(downloadBtn);overlay.appendChild(copyBtn);document.body.appendChild(overlay);console.log('Control buttons added. Text length:',pageText.length);}function downloadText(text){const currentUrl=document.location.href;const pathParts=currentUrl.split('/');const lastPart=pathParts[pathParts.length-1].split('?')[0];const filename=lastPart?`${lastPart}.txt`:'github-content.txt';const blob=new Blob([text],{type:'text/plain'});const url=URL.createObjectURL(blob);const link=document.createElement('a');link.href=url;link.download=filename;document.body.appendChild(link);link.click();document.body.removeChild(link);URL.revokeObjectURL(url);console.log('Download triggered with filename:',filename);}function copyToClipboard(text,button){navigator.clipboard.writeText(text).then(()=>{const originalText=button.textContent;button.textContent='Copied!';button.style.background='#6c757d';setTimeout(()=>{button.textContent=originalText;button.style.background='#28a745';},2000);console.log('Text copied to clipboard');}).catch(err=>{console.error('Failed to copy text: ',err);});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',initializePageHandler);}else{initializePageHandler();}})();
```

   **Recommended**: Use the [Bookmarklet Maker](https://caiorss.github.io/bookmarklet-maker/) for easier installation!

2. **Using the bookmarklet**:
   - Navigate to any GitHub repository page (public repositories work best)
   - Click your "Click 'n' RepoTxt" bookmark
   - The page will automatically redirect to process the repository contents
   - Once loaded, you'll see **Download** and **Copy** buttons in the top-right corner
   - **Download**: Saves the repo contents as a `.txt` file (named after the repo)
   - **Copy**: Copies all content to your clipboard for pasting elsewhere

### Features:
- ✅ **One-click operation** - Just bookmark and click
- ✅ **Smart file naming** - Downloads use the repository name (e.g., `my-repo.txt`)
- ✅ **Multiple output options** - Download as file OR copy to clipboard
- ✅ **Branch support** - Works with main/master branches and specific paths
- ✅ **Plain text format** - Perfect for LLM analysis, documentation, or code review
- ✅ **No server required** - Uses the uithub.com service (free tier available)

### How it works:
1. **URL conversion**: Converts GitHub URLs to [uithub.com](https://uithub.com/) format for text extraction
2. **Content processing**: uithub.com fetches and flattens the repository structure  
3. **User interface**: Adds convenient download/copy buttons to the processed page
4. **File handling**: Intelligently names downloads and provides clipboard functionality

### Troubleshooting:
- **"Not a GitHub URL" error**: Make sure you're on a GitHub repository page
- **No buttons appear**: Wait for the uithub.com page to fully load, then refresh if needed
- **Large repo issues**: Try navigating to a specific folder/branch to reduce size
- **Download not working**: Check your browser's download settings and popup blockers

### Credits
Special thanks to [uithub.com](https://uithub.com/) for providing the excellent GitHub repository content extraction API that makes this tool possible.

---

*If this tool has been helpful to you, consider starring this repository! ⭐*
