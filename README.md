# SprintSync


# Paths for selected ANSYS images
ansys_paths = [
    '/mnt/data/Directional Deformation (captured).png',
    '/mnt/data/Equivalent Stress (captured).png',
    '/mnt/data/Factor of Safety (captured).png',
    '/mnt/data/Total Deformation (captured).png'
]

# Combine all images (ANSYS + Prototype)
all_images = ansys_paths + [
    '/mnt/data/3-D Printed .jpg',
    '/mnt/data/front-view.jpg',
    '/mnt/data/Side-view.jpg'
]

# Output watermarked image paths
watermarked_paths = []

# Apply watermark to all
for i, path in enumerate(all_images):
    out_file = f"/mnt/data/watermarked_{i+1}.jpg"
    add_watermark(path, out_file)
    watermarked_paths.append(out_file)

# Prepare README.md content with Markdown image embedding
readme_content = """# SprintSync – Development Documentation

This repository records the non-confidential technical progress for the SprintSync system.  
Core algorithms, proprietary design specifications, and manufacturing IP are intentionally excluded.  

## Summary of Work

### 1. Simulation & Analysis
- Conducted **structural simulations** in ANSYS, covering:
  - Directional deformation (multi-axis evaluation).
  - Equivalent stress (von-Mises) distribution mapping.
  - Factor of safety validation under load conditions.
  - Total deformation patterns in various orientations.
- Identified critical stress zones and displacement trends for design refinement.

#### Selected Simulation Outputs (Watermarked)
"""

# Add ANSYS watermarked images to README
for path in watermarked_paths[:4]:
    filename = os.path.basename(path)
    readme_content += f"![Simulation]({filename})\n"

readme_content += """

### 2. Mechanical Design & Detailing
- Created detailed CAD models for modular system components.
- Designed **telescopic and tripod structures** with integrated mounting points.
- Incorporated **magnetic alignment and conduction** features for module docking.
- Developed internal component holders using clips, grommets, and cable management sleeves.

### 3. Prototyping & Iterations
- Produced scaled and full-size physical prototypes.
- Performed design-for-assembly (DFA) checks for manufacturability.
- Integrated cable routing and internal protection elements into the structure.

#### Prototype Images (Watermarked)
"""

# Add prototype watermarked images to README
for path in watermarked_paths[4:]:
    filename = os.path.basename(path)
    readme_content += f"![Prototype]({filename})\n"

readme_content += """

---
**Note:** All images are watermarked and not to scale.  
"""

# Save README.md file
readme_path = "/mnt/data/README.md"
with open(readme_path, "w") as f:
    f.write(readme_content)

readme_path, watermarked_paths
