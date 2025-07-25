# Module 2 Challenge: Portfolio Website

## Challenge Overview
Create a simple Docker Compose setup that hosts a portfolio website using Nginx. This challenge will test your understanding of Docker Compose, volumes, and basic web hosting.

## Scenario
You want to create a portfolio website to showcase your Docker skills.

## What You'll Build
A simple static website with:
- **Web Server**: Nginx serving static HTML/CSS files
- **Content**: Some general information
- **Persistence**: Files stored in volumes
- **Access**: Available via web browser on port 80 (or any other if port 80 is already taken on your system)
## Challenge Objectives
### Suggested Project Structure

Organize your project directory as follows:

```
challenge/
├── docker-compose.yml       # Docker Compose configuration file
├── website/                 # Directory for website files
│   ├── index.html           # Main HTML file for the portfolio website
│   └── style.css            # Optional CSS file for styling
└── README.md                # Documentation with setup and usage instructions
```

#### Explanation:
- **`docker-compose.yml`**: Defines the Nginx service and volume mappings for hosting the website.
- **`website/`**: Contains all the static content for the portfolio website.
    - **`index.html`**: The main HTML file showcasing your portfolio.
    - **`style.css`**: Optional CSS file for styling the website.
- **`README.md`**: Provides clear instructions on how to set up, run, and test the project.

### 1. Website Content Files
Create the following files in a `website/` directory:

#### `index.html` - Your portfolio page (Feel free to adjust it)
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Simple Website</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>Welcome to My Website</h1>
        <p>A simple static website example</p>
    </header>
    
    <main>
        <section class="about">
            <h2>About Me</h2>
            <p>Hello! I'm learning how to build and host websites using Docker and Nginx.</p>
        </section>
    </main>
    
    <footer>
        <p>&copy; 2025 My Simple Website</p>
    </footer>
</body>
</html>
```

#### `style.css` - Basic styling (Feel free to adjust it)
```css
body {
    font-family: Arial, sans-serif;
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
    line-height: 1.6;
}

header {
    text-align: center;
    background: #f4f4f4;
    padding: 20px;
    border-radius: 5px;
    margin-bottom: 30px;
}

section {
    margin-bottom: 30px;
}

.skills ul, .bootcamp ul {
    background: #f9f9f9;
    padding: 15px;
    border-radius: 5px;
}

footer {
    text-align: center;
    border-top: 1px solid #ddd;
    padding-top: 20px;
    margin-top: 40px;
}
```

## Getting Started

### Step 1: Create Your Project Structure
```bash
# Navigate to challenge directory
cd ~/bootcamp-docker-cli-day/module-2-docker/challenge

# Create website directory
mkdir website

# Create your portfolio files
nano website/index.html
nano website/style.css  # optional
```

### Step 2: Create Docker Compose File
```bash
# Create your compose configuration
nano docker-compose.yml

# Fill the docker compose file content!
```


### Step 3: Test Your Portfolio
```bash
# Start your portfolio website
docker-compose up -d

# Check if it's running
docker-compose ps

# View your portfolio
curl http://localhost:80
# Or open http://localhost in your browser

# View logs if needed
docker-compose logs

# Stop when done
docker-compose down
```

## Testing Your Solution

### Basic Functionality Tests
```bash
# Test website loads
curl http://localhost:80

# Test container restart
docker-compose down
docker-compose up -d
curl http://localhost:80

# Test file updates (optional)
echo "<p>Updated content</p>" >> website/index.html
# Refresh browser to see changes
```

## Common Issues and Solutions

### Website Not Loading
```bash
# Check if service is running
docker-compose ps

# Check logs for errors
docker-compose logs web

# Verify port mapping
docker-compose config
```

### File Changes Not Showing
```bash
# Restart nginx to reload files
docker-compose restart web

# Or use bind mount with proper permissions
# Make sure your website/ directory exists
```

### Port Already in Use
```bash
# Check what's using port 80
sudo lsof -i :80

# Change port in docker-compose.yml
ports:
  - "8080:80"  # Use port 8080 instead
```

## Submission Guidelines

### What to Submit

When complete, your challenge directory should contain:

1. **Required Files**
   - `website/index.html` - Your portfolio webpage
   - `website/style.css` - CSS styling (optional)
   - `docker-compose.yml` - Docker Compose configuration
   - `README.md` - Setup and usage instructions

### Email Requirements
- **To**: [instructor-email@company.com]
- **Subject**: `[Bootcamp] Module 2 Submission - [Your Name]`
- **Body**: Include the template below

### Email Template
```
Subject: [Bootcamp] Module 2 Submission - [Your Full Name]

Dear Instructor,

I am submitting my completed Module 2: Docker work for the Docker CLI Bootcamp.

Student Information:
- Name: [Your Full Name]
- Time Spent: [Approximate hours]

Additional Features Implemented:
[Any bonus features you added]

Additional Comments:
[Any additional feedback or comments about the challenge]

Best regards,
[Your Name]
```

### File Packaging

#### Option 1: Zip Archive (Recommended)
```bash
# Create submission archive
cd ~/bootcamp-docker-cli-day/module-2-docker
zip -r module2_submission_[yourname].zip challenge/ -x "*.git*"

# Verify archive contents
unzip -l module2_submission_[yourname].zip
```

#### Option 2: Individual File Attachments
If zip is not available, attach files individually with clear naming:
- `[yourname]_docker-compose.yml`
- `[yourname]_index.html`
- `[yourname]_README.md`

### Quality Checklist

Before submitting, verify your work meets these criteria:

#### Functionality
- [ ] Website loads successfully at http://localhost:80
- [ ] Docker Compose file works correctly
- [ ] Website content persists after container restart
- [ ] Service starts and stops cleanly

### Evaluation Criteria

Your submission will be evaluated on:

#### Functionality (50%)
- Website loads and displays correctly
- All required content is present
- Docker Compose works as expected
- Service restarts successfully

#### Content Quality (30%)
- Personal information is complete
- Professional presentation
- Clear demonstration of learning
- Contact information provided

#### Technical Implementation (20%)
- Proper Docker Compose syntax
- Correct volume mapping
- Appropriate service configuration
- Clean documentation

### Pre-Submission Testing
```bash
# Test your complete solution
cd challenge/
docker-compose down -v
docker-compose up -d
curl http://localhost:80
docker-compose down
```

Good luck with your challenge!