# Fun React Quiz App
A React quiz application related to trivia knowledge which generates random questions, developed using React App and TypeScript with Styled-Components scaffolding components using React and TypeScript documentation.<br/><hr>
`NOTE: Synced all stages to avoid untracked files when commiting on Vscode .Git`<br/>
# Functionalities/Demo
[fun react quiz app overview-1.PNG](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/fun%20react%20quiz%20app%20overview-1.png)<br/> 
[fun react quiz app overview-2.PNG](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/fun%20react%20quiz%20app%20overview-2.png)<br/>
- Each quiz question will display 4 choices for users to choose.
- The correct/incorrect answer will be revealed after the user clicks on one choice from four. 
- The quiz will move on to next question after the user is done answering the current one.
# Developing Tools
[Create React App adding TypeScript Docs](https://create-react-app.dev/docs/adding-typescript/)<br/>
[Vscode 1.72](https://code.visualstudio.com/updates/v1_72)<br/>
[Styled-Components Dependency for React](https://styled-components.com/)<br/>
[Unsplash Image Gallery](https://unsplash.com/photos/3FA80_d8rHo)<br/>
[Google Fonts Catamaran Bold700](https://fonts.google.com/specimen/Catamaran?query=catam)<br/>
[Trivia API](https://opentdb.com/api_config.php)<br/>
[vscode-styled-components extension v1.7.5](https://marketplace.visualstudio.com/items?itemName=styled-components.vscode-styled-components)<br/>
# Build
[Prerequisites & Setup](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/README.md#prerequisites--setup)<br/>
[Method Running The Project(Locally)](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/README.md#method-running-the-projectlocally)<br/> 
[Debugging&Troubleshooting](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/README.md#debuggingtroubleshooting)<br/> 
[Synchronous Developing Notes](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/README.md#synchronous-developing-notes)<br/> 
[Testing Results](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/README.md#testing-results)<br/>
# Contribution
[Author]()
# Compatibility
`Windows 10`,` MacBook OS Monterey 12.6`, `Safari`, `Chrome`, `Linux-Ubuntu`
# Method Running The Project(Locally)
Download the entire project to local directory<br/> 
On local device Console, use cd to locate to the project<br/> 
On local Console, run `npm start` to test the project on `localhost:3000`. 
# Prerequisites & Setup
Install all TypeScript documentations within Create React App in local Console:
```
npx create-react-app fun-react-quiz-app --template typescript
```
Navigate into the Fun React Quiz App folder:
```
cd fun-react-quiz-app
```
Open the project with Vscode and remove 6 unnecessary files:
```
setupTests.ts serviceWorker.ts logo.svg index.css App.test.tsx App.css
```
Install the Styled-Components Dependency for React in Console:
```
npm i styled-components @types/styled-components
```
Installed the style-components library first, then installed the styled-component itself.<br/>
Start localhost web server with:
```
npm start
```
Import Catamaran font into [index.html](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/public/index.html):
```JavaScript 
<link href="https://fonts.googleapis.com/css2?family=Catamaran:wght@700&disp lay=swap" rel="stylesheet">
```
Generate a Multiple Choice API from Trivia API to get JSON response.
# Synchronous Developing Notes
## ***Implement Logics:***
Create [API.ts](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/src/API.ts) to create logic for fetching data from API.<br/>
Create [utils.ts](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/src/utils.ts) to randomize the answers to the quiz questions.<br/>
Implement core components in [App.tsx](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/src/App.tsx):
```TypeScript 
 <div className="App">
      <h1>Fun React Quiz</h1>
       <button className = "start" onClick = {startTrivia}>
        Start
      </button>
      <p className = "score">Score:</p>
      <p>Loading Questions...</p>
```
Button to keep the next question in QuestionCard:
```typescript 
    <button className='next' onClick={nextQuestion}>
       NextQuestion
</button>
```
## ***Create QuestionCards components:***
In [QuestionCard.tsx](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/src/components/QuestionCard.tsx), create props for question cards components:
```typescript 
 type Props = {
    question: string;
    answers: string[];
    callback: any;
    userAnswer: any;
    questionNr: number;
    totalQuestions: number; }
```
Create different use states in App.tsx:
```typescript 
const App = () => {
  const [loading, setLoading] = useState(false);
  const [questions, setQuestions] = useState([]);
  const [number, setNumber] = useState(0);
  const [userAnswers, setUserAnswers] = useState([]);
  const [score, setScore] = useState(0);
  const [gameOver, setGameOver] = useState(true);
```
Create the function that grabs the data from API in [API.ts](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/src/API.ts):
```typescript 
 export const fetchQuizQuestions = async (amount: number, difficulty:
Difficulty) => {
    const endpoint = `...`
    const data = await (await fetch(endpoint)).json();
    console.log(data);
```
Now the initial page of React app in localhost server looks like:<br/>
[quiz app initial page.PNG](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/quiz%20app%20initial%20page.png)<br/>
Specify the type in [App.tsx](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/src/App.tsx):
```typescript
export type Question = {
    category: string;
    correct_answer: string;
    difficulty: string;
    incorrect_answer: string[];
    question: string;
    type: string; }
```
Shuffle arrays and functions to export in [utils.ts](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/src/utils.ts):
```typescript 
export const shuffleArray = (array: any[]) =>
    [...array].sort(() => Math.random() - 0.5);
```
Now reload the web server we have Promises showing up on the JS console inspect:<br/>
[Promise shows up in Console Inspecting.PNG](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/Promise%20shows%20up%20in%20Console%20Inspecting.png)<br/>























# Debugging&Troubleshooting
# Testing Results
[quiz app initial page.PNG](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/quiz%20app%20initial%20page.png)<br/>
[Promise shows up in Console Inspecting.PNG](https://github.com/KrystalZhang612/FunReactQuiz/blob/newbranch/Promise%20shows%20up%20in%20Console%20Inspecting.png)<br/>








