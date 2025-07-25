# Module 1: Self Practice - CLI and Terminal Skills

## Introduction
This self-practice section will guide you through essential CLI operations step-by-step. Each exercise builds upon the previous one, preparing you for the final challenge.

## Exercise 1: Basic Navigation and File Operations

### Objective
Master basic file system navigation and file manipulation commands.

### Step-by-Step Instructions

#### Step 1: Create a workspace
```bash
# Create and navigate to your workspace
mkdir -p ~/bootcamp-cli-practice
cd ~/bootcamp-cli-practice

# Verify your location
pwd
```

#### Step 2: Create directory structure
```bash
# Create multiple directories
mkdir -p logs/{api1,api2,api3}
mkdir -p reports
mkdir -p temp

# Verify structure
tree . || ls -la
```

#### Step 3: Create sample files
```bash
# Create empty log files
touch logs/api1/app.log
touch logs/api2/service.log
touch logs/api3/gateway.log

# Create a simple text file
echo "CLI Practice Session" > reports/session_info.txt

# List all created files
find . -type f
```

#### Step 4: File manipulation
```bash
# Copy files
cp reports/session_info.txt temp/backup.txt

# Move files
mv temp/backup.txt temp/session_backup.txt

# Check file sizes
ls -lh temp/
```

### Verification
Your directory structure should look like:
```
bootcamp-cli-practice/
├── logs/
│   ├── api1/app.log
│   ├── api2/service.log
│   └── api3/gateway.log
├── reports/session_info.txt
└── temp/session_backup.txt
```

## Exercise 2: Text Processing Fundamentals

### Objective
Learn to process and analyze text files using CLI tools.

### Step-by-Step Instructions

#### Step 1: Create sample log data
```bash
# Navigate to your workspace
cd ~/bootcamp-cli-practice

# Create sample log entries for API1
cat > logs/api1/app.log << 'EOF'
2024-07-25 10:00:01 INFO API1 Request processed successfully - user123
2024-07-25 10:00:05 ERROR API1 Database connection failed - user456
2024-07-25 10:00:10 INFO API1 Request processed successfully - user789
2024-07-25 10:00:15 WARN API1 Slow response time detected - user123
2024-07-25 10:00:20 INFO API1 Request processed successfully - user456
2024-07-25 10:00:25 ERROR API1 Authentication failed - user999
EOF

# Create sample log entries for API2
cat > logs/api2/service.log << 'EOF'
2024-07-25 10:01:01 INFO API2 Service started successfully
2024-07-25 10:01:05 INFO API2 Request processed successfully - order001
2024-07-25 10:01:10 ERROR API2 Payment processing failed - order002
2024-07-25 10:01:15 INFO API2 Request processed successfully - order003
2024-07-25 10:01:20 ERROR API2 Service unavailable - order004
2024-07-25 10:01:25 INFO API2 Request processed successfully - order005
EOF

# Create sample log entries for API3
cat > logs/api3/gateway.log << 'EOF'
2024-07-25 10:02:01 INFO API3 Gateway initialized
2024-07-25 10:02:05 INFO API3 Request routed successfully - req001
2024-07-25 10:02:10 INFO API3 Request routed successfully - req002
2024-07-25 10:02:15 ERROR API3 Route not found - req003
2024-07-25 10:02:20 WARN API3 High traffic detected
2024-07-25 10:02:25 INFO API3 Request routed successfully - req004
EOF
```

#### Step 2: Basic text analysis
```bash
# Count lines in each log file
echo "=== Line counts ==="
wc -l logs/*/*.log

# Display first few lines
echo "=== First 3 lines of API1 ==="
head -n 3 logs/api1/app.log

# Display last few lines
echo "=== Last 3 lines of API2 ==="
tail -n 3 logs/api2/service.log
```

#### Step 3: Pattern searching with grep
```bash
# Find all ERROR entries
echo "=== All ERROR entries ==="
grep "ERROR" logs/*/*.log

# Find all successful requests
echo "=== All successful requests ==="
grep "successfully" logs/*/*.log

# Count ERROR entries per file
echo "=== ERROR count per file ==="
grep -c "ERROR" logs/*/*.log
```

#### Step 4: Advanced text processing
```bash
# Extract just the API names and log levels
echo "=== API names and log levels ==="
grep -o "INFO API[0-9]" logs/*/*.log | sort | uniq -c

# Find all unique users/orders/requests
echo "=== Unique identifiers ==="
grep -o "user[0-9]*\|order[0-9]*\|req[0-9]*" logs/*/*.log | sort | uniq
```

### Verification Commands
```bash
# Verify all files have content
for file in logs/*/*.log; do
    echo "File: $file ($(wc -l < $file) lines)"
done

# Verify grep functionality
grep -c "INFO\|ERROR\|WARN" logs/*/*.log
```

## Exercise 3: Log Analysis

### Objective
Create automated scripts to analyze log files and generate reports.

### Step-by-Step Instructions

#### Step 1: Create analysis script
```bash
# Create a log analysis script
cat > reports/analyze_logs.sh << 'EOF'
#!/bin/bash

echo "=== Log Analysis Report ==="
echo "Generated on: $(date)"
echo "================================"

# Function to analyze a single log file
analyze_file() {
    local file=$1
    local api_name=$(basename $(dirname $file))
    
    echo "API: $api_name"
    echo "File: $file"
    echo "Total entries: $(wc -l < $file)"
    echo "INFO entries: $(grep -c 'INFO' $file)"
    echo "ERROR entries: $(grep -c 'ERROR' $file)"
    echo "WARN entries: $(grep -c 'WARN' $file)"
    echo "--------------------------------"
}

# Analyze all log files
for log_file in logs/*/*.log; do
    analyze_file "$log_file"
done

echo "=== Summary ==="
echo "Total log files analyzed: $(find logs -name "*.log" | wc -l)"
echo "Total log entries: $(cat logs/*/*.log | wc -l)"
echo "Total ERROR entries: $(grep -c 'ERROR' logs/*/*.log | awk '{sum+=$1} END {print sum}')"
echo "Total INFO entries: $(grep -c 'INFO' logs/*/*.log | awk '{sum+=$1} END {print sum}')"
EOF

# Make script executable
chmod +x reports/analyze_logs.sh
```

#### Step 2: Run the analysis
```bash
# Execute the analysis script
./reports/analyze_logs.sh

# Save output to a report file
./reports/analyze_logs.sh > reports/analysis_report.txt

# View the generated report
cat reports/analysis_report.txt
```

## Next Steps

You are now ready for the challenge! The skills you've practiced here will be essential for:
- Parsing complex log files
- Extracting specific data patterns
- Generating statistical reports
- Automating repetitive tasks

Proceed to the `challenge/` directory when ready.
