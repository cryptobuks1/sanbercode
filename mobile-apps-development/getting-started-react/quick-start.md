# Quick Start

### Create a new App

**Create React App** adalah cara terbaik untuk memulai pembuatan SPA\(Single Page Application\). Untuk memulai instalasi dibutuhkan versi Node &gt;= 6.

```text
npm install -g create-react-app
create-react-app myApp

cd myApp
npm start
```

### Hello World & Introducing JSX

```javascript
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```

Tag diatas bukan html ataupun string. Itu disebut sebagai JSX dan JSX adalah ekstensi sintaks untuk JavaScript. React mencakup fakta bahwa logika rendering secara inheren digabungkan dengan logika UI lainnya: bagaimana kejadian ditangani, bagaimana keadaan berubah dari waktu ke waktu, dan bagaimana data disiapkan untuk ditampilkan.

#### Menggabungkan Expressions dalam JSX

```javascript
formatName = (user) => {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = (
  <h1>
    Hello, {formatName(user)}!
  </h1>
);

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

### Rendering an Element

Misalkan, ada tag &lt;div&gt; dalam sebuah file html dengan id "root". **React** biasanya menggunakan satu DOM node. Jika menggunakan dalam sebuah aplikasi yang sudah ada, mungkin akan banyak "root" DOM sebanyak yang akan digunakan. Untuk render sebuah **React Element**, maka harus membawa keduanya ke dalam _ReactDOM.render\(\)._

```javascript
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

### React hanya memperbarui apa yang dibutuhkan

```javascript
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById('root'));
}

setInterval(tick, 1000);
```

### Components dan Props

Cara paling sederhana untuk mendefinisikan component adalah dengan function :

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

atau dengen menggunakan **ES6 classes :**

```javascript
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

#### Rendering sebuah Component

untuk render sebuah component dapat menggunakan cara :

```javascript
  ReactDOM.render(<Welcome />, document.getElementById('root'));

  // Or

  const Welcome = <Welcome />

  ReactDOM.render(Welcome, document.getElementById('root'));
```

### Passing Props to a Component

Props adalah property sebuah component. Di **React**, Props ber status immutable\(Read-Only\). Untuk passing data props dalam sebuah component dapat menggunakan cara seperti berikut :

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

### Adding State to Component

State juga property dari component. Perbedaan **Props** dan **State** adalah State mutable atau bisa diubah, tapi tidak bisa di gunakan untuk component lain.

```javascript
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

### React Lifecycle

Lifecycle adalah method dari sebuah component untuk mengetahui fase dari sebuah aplikasi.

```javascript
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

### constructor\(\)

constructor adalah hal pertama yang dibaca sebuah **component**. Dari source code pertama constructor membawa argument props dari luar component dan initial state dalam sebuah **component.**

### render\(\)

fase ini dieksekusi untuk menampilkan tag JSX.

### componentDidMount\(\)

`componentDidMount`adalah fase yang eksekusi setelah **render\(\)**. Dari source code diatas, setelah component ditampilkan. Maka state akan diupdate berdasarkan function **this.tick\(\)**.

### componentWillUnmount\(\)

**componentWillUnmount** adalah fase yang dieksekusi saat component di hapus dari **DOM**.

## Do Not Modify State Directly <a id="do-not-modify-state-directly"></a>

```javascript
// Wrong
this.state.comment = 'Hello';
```

```javascript
// Correct
this.setState({comment: 'Hello'});
```

**Note: State Updates May Be Asynchronous**

