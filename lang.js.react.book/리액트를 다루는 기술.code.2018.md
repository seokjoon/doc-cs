* https://github.com/seokjoon/react-test-r2

## ComFunc
```
const ComFunc = ({foo = 'bar'}) => {
	return (
		<Fragment>{foo}</Fragment>
	);
};
/* const ComFunc = ({foo = 'bar'}) => ( <Fragment>{foo}</Fragment> ); */
```
* 컴포넌트는 함수형으로 표현 가능
* props 데이터는 함수의 파라미터로 기재됨
* 아주 간단할 경우 바로 리턴 내용만 기재할 수 있으며, 다른 statement가 존재할 경우 return() 문이 존재

## EventHandling
``` 
/**
 * https://reactjs.org/docs/events.html
 */
class EventHandling extends Component {

	state = {
		msg: '',
		username: '',
	};

	handleChange = (e) => {
		this.setState({ [e.target.name]: e.target.value })
	};

	handleClick = () => { console.log(this.state.msg + ':' + this.state.username);
		this.setState({ msg: '', username: '' });
	};

	handleKeyPress = (e) => {
		if(e.key === 'Enter')  this.handleClick();
	};

	render() {

		const test1 = (
			<div>
				<input type="text" name="msg" placeholder="msg" value={this.state.msg} onChange={this.handleChange} /><br/>
				<input type="text" name="username" placeholder="username" value={this.state.username} onChange={this.handleChange} onKeyPress={this.handleKeyPress} /><br/>
				<button onClick={this.handleClick}>reset</button><br/>
			</div>
		);

		return (
			<Fragment>
				{ test1 }
			</Fragment>
		);
	}
} 
```
* input, button 등 JSX 요소들에 onClick, onChange, onKeyPress 등의 이벤트 핸들링 속성 배치 가능

## LifeCycle

## LoopMap

## PropState

## Styling

## TestTodoList