# ~/.bashrc: executed by bash for non-login shells.

# Source global definitions
if [ -f /etc/bashrc ]; then
    . /etc/bashrc
fi

# Set the default editor to vim
export EDITOR=vim

# Base path for the cloned repositories
BASE_REPO_PATH="/scratch/group/llm_research/cpu-llm-optimization"

# Colors for the prompt
RESET='\[\033[0m\]'        # Reset
BOLD='\[\033[1m\]'         # Bold
USER_HOST_COLOR='\[\033[38;5;81m\]'    # Light Blue
DIR_COLOR='\[\033[38;5;214m\]'         # Orange
GIT_COLOR='\[\033[38;5;39m\]'          # Light Cyan
SEPARATOR_COLOR='\[\033[38;5;245m\]'   # Gray

# Symbols for prompt
GIT_BRANCH_SYMBOL='⎇'
SEPARATOR_LEFT='['
SEPARATOR_RIGHT=']'

# Function to get the current Git branch
parse_git_branch() {
    git branch 2>/dev/null | grep '^*' | colrm 1 2
}

# Git branch display in prompt with branch symbol and separators
__git_ps1() {
    local branch=$(parse_git_branch)
    if [ -n "$branch" ]; then
        echo " ${GIT_COLOR}${SEPARATOR_LEFT}${GIT_COLOR}${GIT_BRANCH_SYMBOL} $branch${RESET}${GIT_COLOR}${SEPARATOR_RIGHT}${RESET}"
    fi
}

# Truncate the directory path to show the last 2 segments
PROMPT_DIRTRIM=1

# Custom prompt segments
PROMPT_USER="${USER_HOST_COLOR}${BOLD}\u@\h${RESET}"
PROMPT_DIR="${DIR_COLOR}\w${RESET}"

# Custom PS1 prompt: simple arrow separators and conditional Git segment
PROMPT_COMMAND='export PS1="${PROMPT_USER}${RESET}: ${PROMPT_DIR}${RESET}$(__git_ps1) \$ "'

# Add your personal bin to PATH
export PATH="$HOME/bin:$PATH"

# Function to navigate to a specific branch directory
goto_branch_directory() {
    local branch="$1"
    local directory="${branch}-cpu-llm-optimization"
    if [ -d "$BASE_REPO_PATH/$directory" ]; then
        cd "$BASE_REPO_PATH/$directory" || return
    else
        echo "Directory $BASE_REPO_PATH/$directory does not exist"
    fi
}

# Specific functions to navigate to each branch directory
goto_branch_predictor() {
    goto_branch_directory "branch_predictor"
}

goto_cache() {
    goto_branch_directory "cache"
}

goto_prefetcher() {
    goto_branch_directory "prefetcher"
}

goto_main() {
    goto_branch_directory "main"
}

# Alias for listing files
alias ll='ls -la'

alias results='cd /scratch/group/llm_research/cpu-llm-optimization/results'

# On startup, navigate to the branch_predictor branch directory
goto_branch_predictor

# End of .bashrc
