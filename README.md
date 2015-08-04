# baobab-angular
A state handling library for Angular, based on Baobab

```js
angular.module('app', ['baobab'])
  .tree('myTree', function() {
    return {
      todos: ['default'],
      num: 1
    };
  })
  .controller('MainCtrl', function($scope, myTree) {

    var vm = this;

    // get cursor references for operations
    var todos = myTree.select('todos');
    var num = myTree.select('num');
    
    // get the values
    vm.todos = todos.get();
    vm.num = num.get();
    
    todos.on('update', onUpdate);
    num.on('update', onUpdate);
    vm.addToto = addTodo;
    
    addTodo('bar');
    addTodo();
    setNum(2);
    setNum();

    function addTodo(val) {
      val = val || 'no value provided!';
      todos.push(val);
    }
    
    function setNum(val) {
      val = val || null;
      // updating a primitive
      num.apply(function() { return val; });
    }

    function onUpdate() {
      vm.todos = todos.get();
      vm.num = num.get();
    }

  });
```
