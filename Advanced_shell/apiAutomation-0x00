#!/bin/bash

#############################################################################
# Task 0: API Request Automation
# Objective: Automate API requests to fetch Pokémon data and handle errors
# 
# This script:
# 1. Makes a request to the Pokémon API for Pikachu
# 2. Saves the response to data.json
# 3. Logs any errors to errors.txt
#############################################################################

# Configuration
POKEMON_NAME="pikachu"
API_URL="https://pokeapi.co/api/v2/pokemon/${POKEMON_NAME}"
OUTPUT_FILE="data.json"
ERROR_FILE="errors.txt"
TIMEOUT=10

# Colors for output (optional but helpful)
GREEN='\033[0;32m'
RED='\033[0;31m'
NC='\033[0m' # No Color

echo "========================================"
echo "Pokémon API Request Automation - Task 0"
echo "========================================"
echo "Target: ${POKEMON_NAME}"
echo "Endpoint: ${API_URL}"
echo ""

# Make the API request
echo "Making API request to ${API_URL}..."

# Use curl to fetch data with timeout and follow redirects
# -s: silent mode (no progress bar)
# -w: write out HTTP status code to a variable
# -o: output to file
HTTP_STATUS=$(curl -s -w "%{http_code}" -o "${OUTPUT_FILE}" \
  --connect-timeout ${TIMEOUT} \
  --max-time $((TIMEOUT * 2)) \
  "${API_URL}" 2>&1)

# Check if curl command was successful
CURL_EXIT_CODE=$?

# Handle network/connection errors
if [ ${CURL_EXIT_CODE} -ne 0 ]; then
  ERROR_MSG="[$(date '+%Y-%m-%d %H:%M:%S')] CURL ERROR: Connection failed (exit code: ${CURL_EXIT_CODE}) for ${POKEMON_NAME}"
  echo -e "${RED}✗ ${ERROR_MSG}${NC}"
  echo "${ERROR_MSG}" >> "${ERROR_FILE}"
  rm -f "${OUTPUT_FILE}"
  exit 1
fi

# Handle HTTP errors based on status codes
if [ "${HTTP_STATUS}" -eq 200 ]; then
  echo -e "${GREEN}✓ Request successful (HTTP 200)${NC}"
  echo "Response saved to: ${OUTPUT_FILE}"
  
  # Validate JSON format
  if command -v jq &> /dev/null; then
    if jq empty "${OUTPUT_FILE}" 2>/dev/null; then
      echo -e "${GREEN}✓ JSON validation passed${NC}"
      
      # Extract and display some basic info
      POKEMON_ID=$(jq '.id' "${OUTPUT_FILE}")
      BASE_EXP=$(jq '.base_experience' "${OUTPUT_FILE}")
      echo ""
      echo "Basic Info:"
      echo "  ID: ${POKEMON_ID}"
      echo "  Base Experience: ${BASE_EXP}"
      echo ""
    else
      ERROR_MSG="[$(date '+%Y-%m-%d %H:%M:%S')] JSON_ERROR: Invalid JSON format in response for ${POKEMON_NAME}"
      echo -e "${RED}✗ ${ERROR_MSG}${NC}"
      echo "${ERROR_MSG}" >> "${ERROR_FILE}"
      exit 1
    fi
  fi
  
elif [ "${HTTP_STATUS}" -eq 404 ]; then
  ERROR_MSG="[$(date '+%Y-%m-%d %H:%M:%S')] HTTP 404: Pokémon '${POKEMON_NAME}' not found"
  echo -e "${RED}✗ ${ERROR_MSG}${NC}"
  echo "${ERROR_MSG}" >> "${ERROR_FILE}"
  rm -f "${OUTPUT_FILE}"
  exit 1
  
elif [ "${HTTP_STATUS}" -eq 429 ]; then
  ERROR_MSG="[$(date '+%Y-%m-%d %H:%M:%S')] HTTP 429: Rate limit exceeded for ${POKEMON_NAME}"
  echo -e "${RED}✗ ${ERROR_MSG}${NC}"
  echo "${ERROR_MSG}" >> "${ERROR_FILE}"
  rm -f "${OUTPUT_FILE}"
  exit 1
  
elif [ "${HTTP_STATUS}" -ge 500 ]; then
  ERROR_MSG="[$(date '+%Y-%m-%d %H:%M:%S')] HTTP ${HTTP_STATUS}: Server error for ${POKEMON_NAME}"
  echo -e "${RED}✗ ${ERROR_MSG}${NC}"
  echo "${ERROR_MSG}" >> "${ERROR_FILE}"
  rm -f "${OUTPUT_FILE}"
  exit 1
  
else
  ERROR_MSG="[$(date '+%Y-%m-%d %H:%M:%S')] HTTP ${HTTP_STATUS}: Unexpected status code for ${POKEMON_NAME}"
  echo -e "${RED}✗ ${ERROR_MSG}${NC}"
  echo "${ERROR_MSG}" >> "${ERROR_FILE}"
  rm -f "${OUTPUT_FILE}"
  exit 1
fi

echo "========================================"
echo "Task 0 completed successfully!"
echo "========================================"
