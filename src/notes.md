// ** the purpose of this App to make the user add their own tasks with the ability to delete any one of it  

// here used ES6 modules system.
// import the useState Hook from React package and 
// css style from local file
import React, { useState } from "react";
import "./styles.css";

// make App function as default for using the App component to other modules 
// this function will return input form to make new to-do item when clicked then able  to delete it  
export default function App() {
   
  // Declare a new state variable, call "inputText" , "todoList"
  // return a new value will updating "setInputText" , "setTodoList"
  // make useState hook initialize value as string coz we have here number or word
  const [inputText, setInputText] = useState("");

    // make useState hook initialize value as array
  const [todoList, setTodoList] = useState([]);

  //  function to create array list of input
  const createTodo = e => {
  // to save input value when preventing a browser to handle the submission
     e.preventDefault();
    
    // Declare a variable named newTodoList and set it equal to a new Array object from() the todoList passed into the function.
    // then push input value to the new array (newTodoList) 
    // update the value of todoList to new value coming from newTodoList array 
    // make input empty after submit
    const newTodoList = Array.from(todoList);
    newTodoList.push(inputText);
    setTodoList(newTodoList);
    setInputText("");
  };

   // other solution to make a new array and put the old one to use [...array]
   const createTodo = e => {
    e.preventDefault();
    const newTodoList = [...todoList, inputText]
    setTodoList(newTodoList);
    setInputText("");
  };

 

  // controlled component for input value when it was called on.
  const onTextChange = e => {
    e.preventDefault();
    setInputText(e.target.value);
  };

  // deleted component, to delete an item with what included from the list and return a new newTodoList
  // here we have the value of index but there is another solution  
  const deleteTodo = idx => {
    const newTodoList = todoList.filter( index => index !== idx);
    setTodoList(newTodoList);
  };

  // other solution
  const deleteTodo = id => {
    const newTodoList = [...todoList];
    newTodoList.splice(id, 1); 
     setTodoList(newTodoList);
  };

  // return form and condition 
 // 1- in the form we have The <Fieldset> hook is a way to contain related fields
 // for every submit we call the createTodo function to create a new item came from input value by called onTextChange function
 //2- the condition if we have items return for each item to add a line in the list including the key, add a dash and delete button through passing call deleted function,
 // or if we don't have any item return div included text/paragraph to explain we don't have any item 

 // note: we can use the map to return item and delete this item by change the filter in delete function to return index
 // todoList.filter(index => index !=idx)  and make map return item then callback deleteTodo(item)
 return (
    <div>
      <h1>My To-do App</h1>
      <form onSubmit={createTodo}>
        <fieldset>
          <legend>To-do</legend>
          <label>
            <span>Enter a new To-do item</span>
            <input onChange={onTextChange} value={inputText} />
          </label>
          <input type="submit" value="Create" onClick={createTodo} />
        </fieldset>
      </form>
      <div>
        <h2>My To-dos</h2>
        <ul>
          {todoList.length ? (
            todoList.map((item) => (
              <li key={item}>
                {item} -{" "}
                <button type="button" onClick={() => deleteTodo(item)}>
                  Delete
                </button>
              </li>
            ))
          ) : (
            <div>No To-do items available</div>
          )}
        </ul>
      </div>
    </div>
  );
}
