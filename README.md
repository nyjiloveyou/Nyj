from pathlib import Path
import zipfile

# Create a sample structure for the nyji online store
project_root = Path("/mnt/data/nyji_store_dark_theme")
assets = {
    "index.html": """
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>nyji | Local T-Shirt Brand</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <header>
    <div class="logo">nyji</div>
    <nav>
      <a href="#">Home</a>
      <a href="#">Shop</a>
      <a href="#">About</a>
      <a href="#">Contact</a>
      <button id="langToggle">ខ្មែរ</button>
    </nav>
  </header>

  <section class="hero">
    <h1>Wear Your Vibe.</h1>
    <p>Local style meets global energy.</p>
    <button>Shop Now</button>
  </section>

  <section class="products">
    <h2>Featured T-Shirts</h2>
    <div class="product-grid">
      <div class="product-card">
        <img src="shirt1.png" alt="T-Shirt 1">
        <h3>Midnight Tee</h3>
        <p>$12.00</p>
      </div>
      <div class="product-card">
        <img src="shirt2.png" alt="T-Shirt 2">
        <h3>Street Flow</h3>
        <p>$15.00</p>
      </div>
    </div>
  </section>

  <footer>
    <p>© 2025 nyji. All rights reserved.</p>
  </footer>

  <script src="script.js"></script>
</body>
</html>
""",
    "styles.css": """
body {
  margin: 0;
  font-family: 'Arial', sans-serif;
  background-color: #121212;
  color: #fff;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1em 2em;
  background: #1e1e1e;
}

.logo {
  font-size: 1.5em;
  font-weight: bold;
}

nav a, nav button {
  margin-left: 1em;
  color: #fff;
  text-decoration: none;
  background: none;
  border: none;
  cursor: pointer;
  font-size: 1em;
}

.hero {
  text-align: center;
  padding: 4em 2em;
  background: #222;
}

.hero h1 {
  font-size: 2.5em;
}

.products {
  padding: 2em;
}

.product-grid {
  display: flex;
  gap: 2em;
  justify-content: center;
  flex-wrap: wrap;
}

.product-card {
  background: #1f1f1f;
  padding: 1em;
  border-radius: 8px;
  width: 200px;
  text-align: center;
}

.product-card img {
  width: 100%;
  border-radius: 4px;
}

footer {
  text-align: center;
  padding: 1em;
  background: #1e1e1e;
}
""",
    "script.js": """
document.getElementById('langToggle').addEventListener('click', () => {
  const current = document.getElementById('langToggle').textContent;
  document.getElementById('langToggle').textContent = current === 'ខ្មែរ' ? 'EN' : 'ខ្មែរ';
});
""",
    "shirt1.png": "",  # Placeholder
    "shirt2.png": ""   # Placeholder
}

# Create the directories and files
project_root.mkdir(parents=True, exist_ok=True)
for filename, content in assets.items():
    file_path = project_root / filename
    if filename.endswith('.png'):
        file_path.touch()  # Create empty placeholder image files
    else:
        file_path.write_text(content.strip())

# Zip the directory
zip_path = Path("/mnt/data/nyji_store_dark_theme.zip")
with zipfile.ZipFile(zip_path, 'w') as zipf:
    for file in project_root.rglob('*'):
        zipf.write(file, file.relative_to(project_root.parent))

zip_path.name
