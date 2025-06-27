<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Terminal Portfolio</title>
    <!-- Link to Google Font: Ubuntu Mono -->
    <link href="https://fonts.googleapis.com/css2?family=Ubuntu+Mono:wght@400;700&display=swap" rel="stylesheet">
    <style>
        /* Overall page styling */
        body {
            margin: 0;
            padding: 0;
            /* Prioritize Ubuntu Mono, then fall back to generic monospace */
            font-family: 'Ubuntu Mono', 'Consolas', 'Liberation Mono', monospace;
            background-color: #000; /* Pure black background for the whole page */
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh; /* Full viewport height */
            overflow: hidden; /* Prevent scrollbars if content doesn't exceed viewport */
            -webkit-font-smoothing: antialiased; /* Better font rendering for macOS */
            -moz-osx-font-smoothing: grayscale; /* Better font rendering for macOS */
        }

        /* Terminal Window Container */
        .terminal-window {
            width: 90%; /* Responsive width */
            max-width: 900px; /* Maximum width for larger screens */
            height: 60vh; /* Responsive height */
            min-height: 300px; /* Minimum height to prevent collapse */
            background-color: #1a1a1a; /* Very dark background for the terminal body */
            border-radius: 8px; /* Slightly rounded corners */
            overflow: hidden; /* Ensures content stays within bounds */
            display: flex;
            flex-direction: column; /* Stacks header and body vertically */
            box-sizing: border-box; /* Include padding and border in the element's total width and height */
        }

        /* Terminal Header (top bar) */
        .terminal-header {
            background-color: transparent; /* No background color, transparent as requested */
            padding: 15px 25px; /* Increased padding for the header */
            display: flex;
            justify-content: space-between; /* Puts title on left, user on right */
            align-items: center; /* Vertically centers items */
            font-size: 0.85em; /* Slightly smaller font size for header text */
            border-bottom: 1px solid #333; /* Subtle separation line, appears more like a border */
            color: #eee; /* Default text color for header items */
        }

        /* Status dot next to title */
        .status-dot {
            display: inline-block;
            width: 8px; /* Size of the dot */
            height: 8px;
            background-color: #009900; /* Less vibrant green for the dot */
            border-radius: 50%; /* Makes it a circle */
            margin-right: 8px; /* Space between dot and title text */
            vertical-align: middle; /* Aligns dot vertically with text */
        }

        /* Terminal Title (left text in header) */
        .terminal-title {
            color: #eee; /* Light gray for the title */
        }

        /* Terminal User (right text in header) */
        .terminal-user {
            color: #009900; /* Less vibrant green for the user@portfolio */
            margin-left: auto; /* Pushes to the right */
        }

        /* Terminal Body (main content area) */
        .terminal-body {
            flex-grow: 1; /* Allows the body to take up remaining vertical space */
            padding: 25px; /* Increased padding inside the terminal body for all sides */
            padding-bottom: 25px; /* Explicitly increased padding at the bottom for the "bottom bar" effect */
            overflow-y: auto; /* Enable vertical scrolling if content overflows */
            color: #009900; /* Less vibrant green text for terminal content */
            font-size: 1em; /* Standard font size for content */
            line-height: 1.4; /* Line spacing */
            display: flex;
            flex-direction: column; /* Arranges lines vertically */
            justify-content: flex-end; /* Pushes the input line to the bottom, creating space above it */
            align-items: center; /* Horizontally centers content within the column */
        }

        /* Container for ASCII art and bio to allow vertical centering above prompt */
        .main-content {
            margin-top: auto; /* Pushes this content block to center vertically above flex-end item */
            margin-bottom: auto; /* Helps in distributing space */
            width: 100%; /* Take full width to allow text-align: center to work */
            text-align: center; /* Ensures content within is horizontally centered */
        }

        /* Individual terminal line (for the prompt) */
        .terminal-line {
            display: flex; /* Arranges prompt and input on one line */
            align-items: baseline; /* Aligns text baselines */
            width: 100%; /* Ensure prompt line also spans width for proper margins */
            padding-top: 15px; /* Add some space above the prompt if main content is small */
        }

        /* Command prompt (e.g., guest@portfolio:~$ ) */
        .prompt {
            color: #009900; /* Less vibrant green for the prompt */
            margin-right: 10px; /* Increased space between prompt and input */
            white-space: nowrap; /* Prevents prompt from wrapping */
        }

        /* Area for user input text */
        .input-area {
            color: #009900; /* Less vibrant green for the input text */
            flex-grow: 1; /* Allows input area to take available space */
            white-space: pre-wrap; /* Preserves whitespace and wraps text */
            outline: none; /* Remove focus outline if this were an actual input field */
            text-align: left; /* Ensure input text starts from left */
        }

        /* Blinking cursor */
        .cursor {
            display: inline-block;
            width: 0.65em; /* Adjusted width to better represent a character block */
            height: 1em; /* Height similar to line height */
            background-color: #009900; /* Less vibrant green cursor */
            margin-left: 5px; /* Small gap between text and cursor */
            animation: blink 1s step-end infinite; /* Blinking animation */
        }

        /* Keyframes for the blinking cursor animation */
        @keyframes blink {
            from, to { background-color: transparent } /* Cursor invisible */
            50% { background-color: #009900; } /* Cursor visible */
        }

        /* ASCII art styling */
        .ascii-art {
            color: #00ff00; /* A brighter green for the ASCII art, similar to the reference image */
            font-family: 'Ubuntu Mono', 'Consolas', 'Liberation Mono', monospace;
            font-size: 0.7em; /* Adjust size as needed for the ASCII font */
            line-height: 0.9; /* Reduce line height for condensed ASCII art */
            margin-bottom: 20px; /* Space between ASCII art and bio */
            /* text-align: center; /* Already handled by .main-content */
            white-space: pre; /* Preserve whitespace and line breaks */
            width: 100%; /* Ensure it spans the width */
            overflow-x: auto; /* Allow horizontal scrolling if ASCII art is too wide */
            padding-bottom: 10px; /* Add some padding if horizontal scrollbar appears */
        }

        /* Bio text styling */
        .bio-text {
            color: #00cc00; /* Consistent with the terminal text color */
            font-size: 0.9em;
            /* text-align: center; /* Already handled by .main-content */
            margin-bottom: 30px; /* Space between bio and input line */
        }
    </style>
</head>
<body>
    <div class="terminal-window">
        <div class="terminal-header">
            <span class="status-dot"></span><span class="terminal-title">terminal-portfolio (dark)</span>
            <span class="terminal-user">guest@portfolio</span>
        </div>
        <div class="terminal-body">
            <!-- New container for content to be centered -->
            <div class="main-content">
                <!-- ASCII Art Name - Provided by User -->
                <pre class="ascii-art">
██████╗ ██╗██╗      █████╗ ██╗         ███████╗██╗██╗  ██╗██╗
██╔══██╗██║██║     ██╔══██╗██║         ██╔════╝██║██║ ██╔╝██║
██████╔╝██║██║     ███████║██║         ███████╗██║█████╔╝ ██║
██╔══██╗██║██║     ██╔══██║██║         ╚════██║██║██╔═██╗ ██║
██████╔╝██║███████╗██║  ██║███████╗    ███████║██║██║  ██╗██║
╚═════╝ ╚═╝╚══════╝╚═╝  ╚═╝╚══════╝    ╚══════╝╚═╝╚═╝  ╚═╝╚═╝
                </pre>
                <!-- Bio Text -->
                <p class="bio-text">
                    Cybersecurity Student at Ibn Zohr University.
                    <br>Dedicated to digital defense | Passionate problem-solver.
                </p>
            </div>

            <div class="terminal-line">
                <span class="prompt">guest@portfolio:~$ </span><span class="input-area">Type a command ...</span><span class="cursor"></span>
            </div>
        </div>
    </div>
</body>
</html>
