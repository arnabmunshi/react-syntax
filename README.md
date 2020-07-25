# react-syntax
Some important Syntax for React

```javascript
import React, { Component } from "react";
import ReactDOM from "react-dom";
import quizService from "./quizService";
import "./assets/style.css";
import QuestionBox from "./components/QuestionBox";
import Result from "./components/Result";

class QuizBee extends Component {
  state = {
    questionBank: [],
    score: 0,
    response: 0,
  };

  getQuestions = () => {
    quizService().then((question) => {
      this.setState({
        questionBank: question,
      });
    });
  };

  componentDidMount() {
    this.getQuestions();
  }

  computeAnswer = (answer, correctAnswer) => {
    if (answer === correctAnswer) {
      this.setState({
        score: this.state.score + 1,
      });
    }
    this.setState({
      response: this.state.response < 5 ? this.state.response + 1 : 5,
    });
  };

  playAgain = () => {
    this.getQuestions();
    this.setState({
      score: 0,
      response: 0,
    });
  };

  render() {
    return (
      <div className="container">
        <div className="title">QuizBee</div>
        {this.state.questionBank.length > 0 &&
          this.state.response < 5 &&
          this.state.questionBank.map(
            ({ question, answers, correct, questionId }) => (
              <QuestionBox
                question={question}
                options={answers}
                key={questionId}
                selected={(answer) => this.computeAnswer(answer, correct)}
              />
            )
          )}

        {this.state.response === 5 ? (
          <Result score={this.state.score} playAgain={this.playAgain} />
        ) : null}
      </div>
    );
  }
}

ReactDOM.render(<QuizBee />, document.getElementById("root"));
```
```javascript
export default (n = 5) =>
  Promise.resolve(qBank.sort(() => 0.5 - Math.random()).slice(0, n));
```
```javascript
var p = Promise.resolve([1,2,3]);
p.then(function(v) {
  console.log(v[0]); // 1
});
```
```javascript
const products = [
  {
    name: "Monitor",
    price: 15000
  },
  {
    name: "Laptop",
    price: 27000
  },
  {
    name: "Table",
    price: 36000
  },
  {
    name: "Mouse",
    price: 300
  },
  {
    name: "Keyboard",
    price: 450
  }
];

const newProducts = products.map(({name, price}, product, index, products) => {
  console.log(name+price);
});
```
```javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.sort(); // Apple,Banana,Mango,Orange
```
```javascript
var points = [40, 100, 1, 5, 25, 10];
points.sort(() => {return 0.5 - Math.random()});
```
```javascript
var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
var citrus = fruits.slice(1, 4); // Orange,Lemon,Apple
```
```javascript
import React, { useState } from "react";

const QuestionBox = ({ question, options, selected }) => {
  const [answer, setAnswer] = useState(options);
  return (
    <div className="questionBox">
      <div className="question">{question}</div>
      {answer.map((text, index) => (
        <button
          className="answerBtn"
          key={index}
          onClick={() => {
            setAnswer([text]);
            selected(text);
          }}
        >
          {text}
        </button>
      ))}
    </div>
  );
};

export default QuestionBox;
```
```javascript
import React from "react";

const Result = ({ score, playAgain }) => {
  return (
    <div className="score-board">
      <div className="score">{score}</div>
      <button className="playBtn" onClick={playAgain}>
        Play Again
      </button>
    </div>
  );
};

export default Result;

```
