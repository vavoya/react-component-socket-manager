# react-component-socket-manager
## 📜 Introduction
**Component Socket Manager** is a lightweight utility designed to simplify and efficiently manage state sharing between React components. This tool applies the concept of socket programming to handle state updates between components but operates entirely within the JavaScript engine, independent of network-based sockets.

## 🚀 Features
- **Socket-like communication** between sibling components or across separate component trees.
- Lightweight and simple to use with minimal boilerplate.
- No need for global state management tools like Redux or Context API.
- Clear and intuitive API: `openSocket`, `sendMessage`, `closeSocket`.

## ❓ What is a Component Socket?
A "Component Socket" is a conceptual tool that enables **local messaging between React components**. Unlike network sockets (e.g., WebSocket), this tool works entirely in the JavaScript engine, managing component state changes efficiently and simply.

## 🛠️ Installation
Copy the `componentSocket.js` file into your project and import the functions where needed:

```javascript
import { openSocket, sendMessage, closeSocket } from './componentSocket';
```

## 📝 Usage Example
Here’s a simple example of how to use the Component Socket Manager in a React project:

```javascript
// Import the socket manager
import { openSocket, sendMessage, closeSocket } from './componentSocket';

// Component A: Opens a socket and listens for messages
const ComponentA = () => {
  const [state, setState] = useState()

  useEffect(() => {
    openSocket(4000, (data) => {
      console.log('ComponentA received:', data)
      setState(data)
    });
    return () => closeSocket(4000); // Clean up the socket when the component unmounts
  }, []);

  return (
    <button onClick={() => sendMessage(4001, 'Hello from ComponentA')}>
      Send Message
    </button>
  );
};

// Component B: Sends a message to the same socket
const ComponentB = () => {
  const [state, setState] = useState()
  useEffect(() => {
    openSocket(4001, (data) => {
      console.log('ComponentB received:', data)
      setState(data)
    });
    return () => closeSocket(4001);
  }, []);

  return (
    <button onClick={() => sendMessage(4000, 'Hello from ComponentB')}>
      Send Message
    </button>
  );
};
```

## 💡 Benefits
- **Simple to use**: Quickly enable sibling component communication without additional setup.
- **Lightweight**: Avoids the complexity of global state management tools.
- **React-friendly**: Designed to work seamlessly with React's lifecycle methods like `useEffect`.

## ❗ Limitations
- **Not a Network Socket**: This tool does not support network communication (e.g., WebSocket).
- **Port Conflicts**: Ensure unique port numbers to avoid conflicts. The tool includes error handling for duplicate ports.

## 💻 Advanced Features (Future Ideas)
- Automatic port management for dynamic socket creation.
- Broadcast messaging to multiple listeners on the same port.
- Enhanced debugging tools for tracking message flow.

## 🛠️ License
This project is licensed under the MIT License.
