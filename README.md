<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Expressions & Everyday Terms</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #6a93cb 0%, #a4bfef 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 1000px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8f4f2);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .word-bank h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(74, 111, 165, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(74, 111, 165, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #4a6fa5;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .option.selected {
            background: #4a6fa5;
            color: white;
            border-color: #4a6fa5;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #4a6fa5;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #4a6fa5;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .match-item.selected {
            background: #e8f4f2;
            border-color: #4a6fa5;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .reset-btn {
            background: linear-gradient(135deg, #f44336, #ff7961);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 10px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(244, 67, 54, 0.3);
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(244, 67, 54, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 24px;
            margin-right: 10px;
            vertical-align: middle;
        }

        /* Vocabulary List Styles */
        .vocabulary-list {
            padding: 20px;
        }

        .vocabulary-item {
            margin-bottom: 25px;
            padding: 20px;
            border-radius: 10px;
            background: #f8f9fa;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        .vocabulary-item h3 {
            color: #4a6fa5;
            margin-bottom: 10px;
            font-size: 1.4em;
            border-bottom: 2px solid #4a6fa5;
            padding-bottom: 8px;
        }

        .vocabulary-item p {
            margin-bottom: 8px;
            line-height: 1.6;
        }

        .example {
            font-style: italic;
            color: #555;
            padding-left: 15px;
            border-left: 3px solid #4a6fa5;
            margin-top: 10px;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/12</div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-book icon"></i> Vocabulary Game: Expressions & Everyday Terms</h1>
            <p>Test your knowledge of these English terms and expressions!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('vocabulary')">Vocabulary List</button>
            <button class="nav-btn" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Definitions</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Vocabulary List Section -->
        <div id="vocabulary" class="game-section active">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Vocabulary Explanations</h2>
            
            <div class="vocabulary-list">
                <div class="vocabulary-item">
                    <h3>at most</h3>
                    <p><strong>Definition:</strong> Not more than; indicating a maximum limit.</p>
                    <p><strong>Usage:</strong> Used to set an upper boundary or limit.</p>
                    <p class="example"><strong>Example:</strong> "The project will take at most two weeks to complete."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>useful</h3>
                    <p><strong>Definition:</strong> Able to be used for a practical purpose or in several ways.</p>
                    <p><strong>Usage:</strong> Describes something that serves a purpose or provides benefit.</p>
                    <p class="example"><strong>Example:</strong> "This app is really useful for organizing my schedule."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>by</h3>
                    <p><strong>Definition:</strong> Not later than; before a specified time.</p>
                    <p><strong>Usage:</strong> Indicates a deadline or time limit.</p>
                    <p class="example"><strong>Example:</strong> "Please submit your report by Friday."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>on the other hand</h3>
                    <p><strong>Definition:</strong> Used to introduce a different or opposing point of view.</p>
                    <p><strong>Usage:</strong> Presents an alternative perspective in a discussion.</p>
                    <p class="example"><strong>Example:</strong> "The job pays well; on the other hand, the hours are very long."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>boring</h3>
                    <p><strong>Definition:</strong> Not interesting; tedious.</p>
                    <p><strong>Usage:</strong> Describes something that fails to hold attention or interest.</p>
                    <p class="example"><strong>Example:</strong> "The lecture was so boring that several people fell asleep."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>a bit</h3>
                    <p><strong>Definition:</strong> A small amount or degree; slightly.</p>
                    <p><strong>Usage:</strong> Used to moderate statements or indicate a small quantity.</p>
                    <p class="example"><strong>Example:</strong> "I'm a bit tired after working all day."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>lonely</h3>
                    <p><strong>Definition:</strong> Sad because one has no friends or company.</p>
                    <p><strong>Usage:</strong> Describes the feeling of isolation or lack of companionship.</p>
                    <p class="example"><strong>Example:</strong> "She felt lonely after moving to a new city where she didn't know anyone."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>if anything</h3>
                    <p><strong>Definition:</strong> Used to suggest tentatively that something may be the case (often the opposite of what has been said).</p>
                    <p><strong>Usage:</strong> Introduces a contrasting or qualifying statement.</p>
                    <p class="example"><strong>Example:</strong> "I'm not disappointed with the result; if anything, I'm pleasantly surprised."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>instead</h3>
                    <p><strong>Definition:</strong> As an alternative or replacement.</p>
                    <p><strong>Usage:</strong> Indicates a substitute or different choice.</p>
                    <p class="example"><strong>Example:</strong> "We didn't go to the beach; instead, we visited the museum."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>can go through</h3>
                    <p><strong>Definition:</strong> To proceed to the next stage; to be approved or accepted.</p>
                    <p><strong>Usage:</strong> Often used in competitive contexts or approval processes.</p>
                    <p class="example"><strong>Example:</strong> "Only the top three teams can go through to the final round."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>marks</h3>
                    <p><strong>Definition:</strong> Grades or scores given for academic work.</p>
                    <p><strong>Usage:</strong> Refers to evaluation results in educational contexts.</p>
                    <p class="example"><strong>Example:</strong> "She received excellent marks on her final exams."</p>
                </div>
            </div>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">at most</span>
                    <span class="word-option">useful</span>
                    <span class="word-option">by</span>
                    <span class="word-option">on the other hand</span>
                    <span class="word-option">boring</span>
                    <span class="word-option">a bit</span>
                    <span class="word-option">lonely</span>
                    <span class="word-option">if anything</span>
                    <span class="word-option">instead</span>
                    <span class="word-option">can go through</span>
                    <span class="word-option">marks</span>
                </div>
            </div>

            <div id="fill-gaps-container">
                <!-- Sentences will be dynamically inserted here -->
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
            <button class="reset-btn" onclick="resetFillBlanks()">Reset Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Match the words with their definitions</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Vocabulary Words</h4>
                    <div class="match-item" data-word="at most" onclick="selectMatch(this)">at most</div>
                    <div class="match-item" data-word="useful" onclick="selectMatch(this)">useful</div>
                    <div class="match-item" data-word="by" onclick="selectMatch(this)">by</div>
                    <div class="match-item" data-word="on the other hand" onclick="selectMatch(this)">on the other hand</div>
                    <div class="match-item" data-word="boring" onclick="selectMatch(this)">boring</div>
                    <div class="match-item" data-word="a bit" onclick="selectMatch(this)">a bit</div>
                    <div class="match-item" data-word="lonely" onclick="selectMatch(this)">lonely</div>
                    <div class="match-item" data-word="if anything" onclick="selectMatch(this)">if anything</div>
                    <div class="match-item" data-word="instead" onclick="selectMatch(this)">instead</div>
                    <div class="match-item" data-word="can go through" onclick="selectMatch(this)">can go through</div>
                    <div class="match-item" data-word="marks" onclick="selectMatch(this)">marks</div>
                </div>
                <div class="match-column">
                    <h4>Definitions</h4>
                    <div id="meanings-container">
                        <!-- Meanings will be dynamically inserted here -->
                    </div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
            <button class="check-btn" onclick="checkMatching()">Check Matching</button>
            <button class="reset-btn" onclick="resetMatching()">Reset Matching</button>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What does "at most" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">At least</div>
                    <div class="option" onclick="selectOption(this, true)">Not more than; maximum limit</div>
                    <div class="option" onclick="selectOption(this, false)">Exactly</div>
                    <div class="option" onclick="selectOption(this, false)">Approximately</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: What does "useful" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Beautiful</div>
                    <div class="option" onclick="selectOption(this, true)">Able to be used for a practical purpose</div>
                    <div class="option" onclick="selectOption(this, false)">Expensive</div>
                    <div class="option" onclick="selectOption(this, false)">Difficult to use</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: What does "by" mean when referring to time?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">After</div>
                    <div class="option" onclick="selectOption(this, true)">Not later than; before a specified time</div>
                    <div class="option" onclick="selectOption(this, false)">During</div>
                    <div class="option" onclick="selectOption(this, false)">At exactly</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: What does "on the other hand" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Additionally</div>
                    <div class="option" onclick="selectOption(this, true)">Used to introduce a different or opposing point of view</div>
                    <div class="option" onclick="selectOption(this, false)">Similarly</div>
                    <div class="option" onclick="selectOption(this, false)">Therefore</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: What does "boring" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Exciting</div>
                    <div class="option" onclick="selectOption(this, true)">Not interesting; tedious</div>
                    <div class="option" onclick="selectOption(this, false)">Colorful</div>
                    <div class="option" onclick="selectOption(this, false)">Fast-paced</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: What does "a bit" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A lot</div>
                    <div class="option" onclick="selectOption(this, true)">A small amount or degree; slightly</div>
                    <div class="option" onclick="selectOption(this, false)">Completely</div>
                    <div class="option" onclick="selectOption(this, false)">Never</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 7: What does "lonely" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Happy with many friends</div>
                    <div class="option" onclick="selectOption(this, true)">Sad because one has no friends or company</div>
                    <div class="option" onclick="selectOption(this, false)">Busy with social activities</div>
                    <div class="option" onclick="selectOption(this, false)">Content with solitude</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 8: What does "if anything" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Definitely</div>
                    <div class="option" onclick="selectOption(this, true)">Used to suggest tentatively something may be the case</div>
                    <div class="option" onclick="selectOption(this, false)">Never</div>
                    <div class="option" onclick="selectOption(this, false)">Always</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 9: What does "instead" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Additionally</div>
                    <div class="option" onclick="selectOption(this, true)">As an alternative or replacement</div>
                    <div class="option" onclick="selectOption(this, false)">At the same time</div>
                    <div class="option" onclick="selectOption(this, false)">Before</div>
                </div>
                <div class="feedback" id="mc-feedback-9" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 10: What does "can go through" mean in a competition?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To be eliminated</div>
                    <div class="option" onclick="selectOption(this, true)">To proceed to the next stage</div>
                    <div class="option" onclick="selectOption(this, false)">To watch the competition</div>
                    <div class="option" onclick="selectOption(this, false)">To organize the event</div>
                </div>
                <div class="feedback" id="mc-feedback-10" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 11: What are "marks" in an educational context?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Teachers</div>
                    <div class="option" onclick="selectOption(this, true)">Grades or scores given for academic work</div>
                    <div class="option" onclick="selectOption(this, false)">Classrooms</div>
                    <div class="option" onclick="selectOption(this, false)">Textbooks</div>
                </div>
                <div class="feedback" id="mc-feedback-11" style="display: none;"></div>
            </div>
            
            <button class="reset-btn" onclick="resetMultipleChoice()">Reset Answers</button>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];
        
        // Track correct answers for each section
        let fillBlanksCorrect = 0;
        let matchingCorrect = 0;
        let multipleChoiceCorrect = 0;
        
        // Definitions for the matching game
        const definitions = [
            { meaning: "at most", text: "Not more than; indicating a maximum limit" },
            { meaning: "useful", text: "Able to be used for a practical purpose" },
            { meaning: "by", text: "Not later than; before a specified time" },
            { meaning: "on the other hand", text: "Used to introduce a different or opposing point of view" },
            { meaning: "boring", text: "Not interesting; tedious" },
            { meaning: "a bit", text: "A small amount or degree; slightly" },
            { meaning: "lonely", text: "Sad because one has no friends or company" },
            { meaning: "if anything", text: "Used to suggest tentatively something may be the case" },
            { meaning: "instead", text: "As an alternative or replacement" },
            { meaning: "can go through", text: "To proceed to the next stage; to be approved" },
            { meaning: "marks", text: "Grades or scores given for academic work" }
        ];

        // Sentences for the fill-in-the-blanks game
        const sentences = [
            { text: "The repair should cost <input type='text' class='fill-blank' data-answer='at most' placeholder='answer'> $100.", answer: "at most" },
            { text: "This multitool is extremely <input type='text' class='fill-blank' data-answer='useful' placeholder='answer'> for camping trips.", answer: "useful" },
            { text: "Please complete the assignment <input type='text' class='fill-blank' data-answer='by' placeholder='answer'> next Monday.", answer: "by" },
            { text: "I'd like to buy a new car; <input type='text' class='fill-blank' data-answer='on the other hand' placeholder='answer'>, it's a significant financial commitment.", answer: "on the other hand" },
            { text: "The documentary was so <input type='text' class='fill-blank' data-answer='boring' placeholder='answer'> that I couldn't finish watching it.", answer: "boring" },
            { text: "Could you turn the music down <input type='text' class='fill-blank' data-answer='a bit' placeholder='answer'>? It's too loud.", answer: "a bit" },
            { text: "After her friends moved away, she felt quite <input type='text' class='fill-blank' data-answer='lonely' placeholder='answer'> in the big city.", answer: "lonely" },
            { text: "I'm not angry about what happened; <input type='text' class='fill-blank' data-answer='if anything' placeholder='answer'>, I'm relieved it's over.", answer: "if anything" },
            { text: "We didn't go to the cinema; <input type='text' class='fill-blank' data-answer='instead' placeholder='answer'>, we watched a movie at home.", answer: "instead" },
            { text: "Only the best performers <input type='text' class='fill-blank' data-answer='can go through' placeholder='answer'> to the final audition.", answer: "can go through" },
            { text: "She received excellent <input type='text' class='fill-blank' data-answer='marks' placeholder='answer'> on all her science exams.", answer: "marks" },
            { text: "The meeting will last <input type='text' class='fill-blank' data-answer='at most' placeholder='answer'> one hour.", answer: "at most" },
            { text: "I find this app very <input type='text' class='fill-blank' data-answer='useful' placeholder='answer'> for learning new vocabulary.", answer: "useful" }
        ];

        // Function to shuffle array (Fisher-Yates algorithm)
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // Initialize the fill-in-the-blanks game with shuffled sentences
        function initFillBlanks() {
            const container = document.getElementById('fill-gaps-container');
            container.innerHTML = '';
            
            // Shuffle the sentences
            const shuffledSentences = shuffleArray([...sentences]);
            
            // Create and append the sentence elements
            shuffledSentences.forEach((sentence, index) => {
                const div = document.createElement('div');
                div.className = 'question';
                div.innerHTML = `
                    <h3>Question ${index + 1}:</h3>
                    <p>${sentence.text}</p>
                    <div class="feedback" id="feedback-${index + 1}" style="display: none;"></div>
                `;
                container.appendChild(div);
            });
        }

        // Initialize the matching game with shuffled definitions
        function initMatchingGame() {
            const meaningsContainer = document.getElementById('meanings-container');
            meaningsContainer.innerHTML = '';
            
            // Shuffle the definitions
            const shuffledDefinitions = shuffleArray([...definitions]);
            
            // Create and append the definition elements
            shuffledDefinitions.forEach(def => {
                const div = document.createElement('div');
                div.className = 'match-item';
                div.setAttribute('data-meaning', def.meaning);
                div.onclick = function() { selectMatch(this); };
                div.textContent = def.text;
                meaningsContainer.appendChild(div);
            });
        }

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
            
            // If showing fill-in-the-blanks section, reinitialize with shuffled sentences
            if (sectionId === 'fill-gaps') {
                initFillBlanks();
            }
            
            // If showing matching section, reinitialize with shuffled definitions
            if (sectionId === 'matching') {
                initMatchingGame();
                // Reset matching game state
                document.querySelectorAll('.match-item').forEach(item => {
                    item.classList.remove('selected', 'matched');
                });
                selectedWord = null;
                selectedMeaning = null;
                matchedPairs = [];
                document.getElementById('matching-feedback').style.display = 'none';
            }
            
            // Update score display
            updateScore();
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            fillBlanksCorrect = correctCount;
            updateScore();
        }

        function resetFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            blanks.forEach(blank => {
                blank.value = '';
                blank.classList.remove('correct', 'incorrect');
            });
            
            const feedbacks = document.querySelectorAll('#fill-gaps .feedback');
            feedbacks.forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            fillBlanksCorrect = 0;
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === definitions.length) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            matchingCorrect = matchedPairs.length;
            updateScore();
        }

        function checkMatching() {
            const allMatches = document.querySelectorAll('.match-item[data-word]');
            let allCorrect = true;
            
            allMatches.forEach(item => {
                if (!item.classList.contains('matched')) {
                    allCorrect = false;
                }
            });
            
            const feedback = document.getElementById('matching-feedback');
            if (allCorrect) {
                feedback.textContent = '🎉 Excellent! All matches are correct!';
                feedback.className = 'feedback correct';
            } else {
                const unmatchedCount = definitions.length - matchedPairs.length;
                feedback.textContent = `You have ${unmatchedCount} unmatched pair${unmatchedCount !== 1 ? 's' : ''}. Keep trying!`;
                feedback.className = 'feedback incorrect';
            }
            feedback.style.display = 'block';
        }

        function resetMatching() {
            document.querySelectorAll('.match-item').forEach(item => {
                item.classList.remove('selected', 'matched');
            });
            
            initMatchingGame();
            
            selectedWord = null;
            selectedMeaning = null;
            matchedPairs = [];
            
            document.getElementById('matching-feedback').style.display = 'none';
            
            matchingCorrect = 0;
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            
            // Count correct answers in multiple choice
            multipleChoiceCorrect = document.querySelectorAll('#multiple-choice .option.correct.selected').length;
            updateScore();
        }

        function resetMultipleChoice() {
            document.querySelectorAll('#multiple-choice .option').forEach(option => {
                option.classList.remove('selected', 'correct', 'incorrect');
            });
            
            document.querySelectorAll('#multiple-choice .feedback').forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            multipleChoiceCorrect = 0;
            updateScore();
        }

        function updateScore() {
            // Total score
            score = fillBlanksCorrect + matchingCorrect + multipleChoiceCorrect;
            document.getElementById('score').textContent = score;
        }
        
        // Initialize the page
        window.onload = function() {
            initFillBlanks();
            initMatchingGame();
        }
    </script>
</body>
</html>
