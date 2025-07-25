# Module 1 Challenge: API Log Analysis

## Challenge Overview
Your task is to analyze log files from multiple APIs to extract success and failure statistics. This challenge will test your CLI skills in a real-world scenario.

## Scenario
You work for a company that operates three critical APIs:
- **UserAPI**: Handles user authentication and profile management
- **PaymentAPI**: Processes payment transactions
- **NotificationAPI**: Manages email and SMS notifications

Each API generates log files throughout the day, and you need to create a comprehensive analysis of their performance.

## Challenge Objectives
Create a solution that analyzes the provided log files and produces:

1. **API Statistics Report** containing:
   - API name
   - Total number of requests
   - Number of successful operations
   - Number of failed operations
   - Success rate percentage
   - Failure rate percentage

## Provided Data

The challenge includes log files for three APIs located in the `data/` directory:
- `data/userapi.log` - User API logs
- `data/paymentapi.log` - Payment API logs  
- `data/notificationapi.log` - Notification API logs

## Log Format

Each log entry follows this format:
```
YYYY-MM-DD HH:MM:SS [LEVEL] API_NAME: MESSAGE - RequestID
```

Example:
```
2024-07-25 14:30:15 [INFO] UserAPI: Authentication successful - REQ_001
2024-07-25 14:30:20 [ERROR] PaymentAPI: Payment processing failed - REQ_002
```

## Success/Failure Criteria

### Success Indicators:
- Log level: `[INFO]`
- Messages containing: "successful", "completed", "processed"

### Failure Indicators:
- Log level: `[ERROR]`
- Messages containing: "failed", "error", "timeout", "rejected"

### Warning Indicators (count but don't include in success/failure):
- Log level: `[WARN]`
- Messages containing: "slow", "retry", "degraded"

## Required Deliverables

### 1. Analysis Script (`analyze_apis.sh`)
Create a bash script that:
- Processes all three log files
- Calculates statistics for each API
- Generates a formatted report
- Outputs results to both console and file

### 2. Summary Report (`api_summary.txt`)
Generate a text report containing:
```
=== API Performance Analysis ===
Generated: [timestamp]

API Statistics:
UserAPI:
  Total Requests: [number]
  Successful: [number] ([percentage]%)
  Failed: [number] ([percentage]%)
  
PaymentAPI:
  Total Requests: [number]
  Successful: [number] ([percentage]%)
  Failed: [number] ([percentage]%)
  
NotificationAPI:
  Total Requests: [number]
  Successful: [number] ([percentage]%)
  Failed: [number] ([percentage]%)

Overall Summary:
  Total System Requests: [number]
  System Success Rate: [percentage]%
  Most Reliable API: [API name]
  Most Problematic API: [API name]
```

## Evaluation Criteria

Your solution will be evaluated on:

1. **Correctness (40%)**
   - Accurate calculation of statistics
   - Proper identification of success/failure patterns
   - Correct handling of edge cases

2. **Code Quality (30%)**
   - Clean, readable shell scripts
   - Proper error handling
   - Good commenting and documentation

3. **Completeness (20%)**
   - All required deliverables present
   - Meets all technical requirements
   - Follows specified output formats

4. **Efficiency (10%)**
   - Optimal use of CLI tools
   - Reasonable performance
   - No unnecessary processing

## Getting Started

1. Navigate to the challenge directory:
   ```bash
   cd ~/bootcamp-docker-cli-day/module-1-cli-terminal/challenge
   ```

2. Examine the provided log files:
   ```bash
   ls -la data/
   head -20 data/userapi.log
   ```

3. Start developing your analysis script:
   ```bash
   nano analyze_apis.sh
   ```

4. Test your script incrementally:
   ```bash
   chmod +x analyze_apis.sh
   ./analyze_apis.sh
   ```

## Hints and Tips

1. **Start Small**: Begin with analyzing one API, then extend to all three
2. **Use Functions**: Break your script into reusable functions
3. **Test Edge Cases**: What happens with empty files or malformed entries?
4. **Validate Results**: Cross-check your calculations manually
5. **Document Everything**: Comment your code and explain your approach

## Submission Guidelines

### What to Submit

When complete, your challenge directory should contain:

1. **Required Files**
   - `analyze_apis.sh` - Your main analysis script
   - `api_summary.txt` - Generated summary report

### Email Requirements
- **To**: [instructor-email@company.com]
- **Subject**: `[Bootcamp] Module 1 Challenge Submission - [Your Name]`
- **Body**: Include the template below

### Email Template
```
Subject: [Bootcamp] Module 1 Challenge Submission - [Your Full Name]

Dear Instructor,

I am submitting my completed Module 1 Challenge for the Docker CLI Bootcamp.

Student Information:
- Name: [Your Full Name]
- Time Spent: [Approximate hours]

Questions or Issues Encountered:
[Describe any problems you faced and how you resolved them]

Additional Comments:
[Any additional feedback or comments]

Best regards,
[Your Name]
```

### File Packaging

#### Option 1: Zip Archive (Recommended)
```bash
# Create submission archive
cd ~/bootcamp-docker-cli-day/module-1-cli-terminal
zip -r module1_challenge_[yourname].zip challenge/ -x "*.git*"

# Verify archive contents
unzip -l module1_challenge_[yourname].zip
```

#### Option 2: Individual File Attachments
If zip is not available, attach files individually with clear naming:
- `[yourname]_analyze_apis.sh`
- `[yourname]_api_summary.txt`

### Quality Checklist

Before submitting, verify your work meets these criteria:

#### Script Quality
- [ ] Scripts are executable (`chmod +x`)
- [ ] Scripts include proper shebang (`#!/bin/bash`)
- [ ] Code is well-commented
- [ ] Scripts handle errors gracefully
- [ ] Output is correctly formatted

#### Functional Requirements
- [ ] All APIs are analyzed correctly
- [ ] Success/failure rates are accurate
- [ ] Reports contain all required information
- [ ] CSV files are properly formatted
- [ ] Scripts process all provided log files

#### File Organization
- [ ] Files are named correctly
- [ ] Directory structure is maintained
- [ ] No temporary or backup files included
- [ ] All required deliverables are present

Good luck with your challenge!
