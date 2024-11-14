# Game Assets Hosting with GitHub Pages

A guide to help setting up a GitHub repository to host game assets (models, textures, shaders, etc.) using **GitHub Pages**.

## 🚀 Getting Started

### 1. **Create a New GitHub Repository** 
- [ ] Go to [GitHub](https://github.com) and create a new repository, `Assets`.

### 2. **Upload Your Assets**

- [ ] Organize your assets in a folder structure like below:
   ```
   game-assets/
   ├── models/
   │   └── robot.glb
   ├── textures/
   │   └── metal_diffuse.png
   └── shaders/
       └── vertex.wgsl
   ```

### 3. **Enable GitHub Pages**

- [ ] Go to the **Settings** of your repository.
- [ ] Scroll down to the **Pages** section.
- [ ] Under **Source**, select the `main` branch (or the branch where your assets are stored) and click **Save**.
- [ ] GitHub will generate a URL for your hosted files. It will look like:
   ```
   https://username.github.io/game-assets/
   ```

### 4. **Accessing Your Assets in the Game**

You can now load your assets using their URLs. For example:

- **Texture URL:** `https://username.github.io/game-assets/textures/metal_diffuse.png`
- **Model URL:** `https://username.github.io/game-assets/models/robot.glb`
- **Shader URL:** `https://username.github.io/game-assets/shaders/vertex.wgsl`

### 5. **Loading Assets with JavaScript**

You can fetch and use these assets in your WebGPU application. Here's an example:

```javascript
// URLs for the assets
const textureUrl = 'https://username.github.io/game-assets/textures/metal_diffuse.png';
const modelUrl = 'https://username.github.io/game-assets/models/robot.glb';
const shaderUrl = 'https://username.github.io/game-assets/shaders/vertex.wgsl';

// Function to load a texture
async function loadTexture(url) {
  const image = new Image();
  image.src = url;
  await image.decode();
  const bitmap = await createImageBitmap(image);
  return bitmap;
}

// Function to load a shader
async function loadShader(url) {
  const response = await fetch(url);
  const shaderCode = await response.text();
  return shaderCode;
}

// Example usage
loadTexture(textureUrl).then((bitmap) => {
  console.log("Texture loaded:", bitmap);
});

loadShader(shaderUrl).then((vertexShaderCode) => {
  console.log("Vertex Shader Code:", vertexShaderCode);
});
```

### 6. **Handling CORS Issues**

GitHub Pages supports CORS by default. However, if you encounter issues:
- Make sure your repository is public.
- Use the full URL (with `https://`).

### 7. **Using Raw URLs (Alternative Method)**

You can also use raw URLs for fetching files directly:
```
https://raw.githubusercontent.com/username/game-assets/main/textures/metal_diffuse.png
```
**Note:** `raw.githubusercontent.com` does not support CORS by default, so using GitHub Pages is usually the better option.

### 8. **Updates and Versioning**

When you update assets in your repository, the changes are automatically reflected on GitHub Pages. If updates don't appear immediately, try clearing your browser cache.

### 9. **Example Asset Fetch URLs**

- **Texture URL:** `https://username.github.io/game-assets/textures/metal_diffuse.png`
- **Model URL:** `https://username.github.io/game-assets/models/robot.glb`
- **Shader URL:** `https://username.github.io/game-assets/shaders/vertex.wgsl`

### 🔄 **Clearing Cache**

If updates to assets are not reflected, you may need to clear the browser cache:
- For most browsers: Press `Ctrl + F5` (Windows/Linux) or `Cmd + Shift + R` (Mac).

### 🔧 **Tips for Larger Projects**

For larger projects or production use, consider dedicated hosting services like:
- AWS S3
- Google Cloud Storage
- Azure Blob Storage
- A CDN for faster global delivery

Happy coding! 🎮🚀
