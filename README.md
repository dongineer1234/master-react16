####################################################################################################

#1 Introduction and Project Setup

# npx로 react application을 생성
: npx create-react-app master-react16

####################################################################################################

#2 Return Types Strings and Fragments

# return types
: 이전의 react에서는 하나의 component에 써서 하나만 return해야 했지만
react16에서는 그럴 필요가 없음

# Fragment
: return fragment를 사용
이전의 span, array 사용 안해도 되고 fragments만 사용하면 됨
span은 사용할 때 CSS와 꼬일 수도 있고 문제가 있음
이점을 fragment가 보완

# strings return types
: return "hello" Application에 전달하여 사용 가능

####################################################################################################

#3 Portals

# Portals
: 사용하면 react <div id="root"/> 밖에 react를 넣어 render

: 다른 page에서 loading할 때 유용

####################################################################################################

#4 Error Boundaries

# Error Boundaries
: App component로 하여금 component children
(지금까지 완성된 코드에서 Portals component, ReturnTypes component)의 error를 관리할 수 있게해줌

# componentDidCatch
: ErrorMaker component(children component)에서의 error를 App component(parent component)에서 잡아냄

# componentDidCatch = (error, info) => {console.log(`catched ${error} the info i have is ${JSON.stringify(info)}`)}
: error는 error 
info는 error information
JSON.stringify(info)는 error의 위치

# {hasError ? <ErrorFallback /> : <ErrorMaker />}
: 이렇게 하는것도 나쁘진 않은데 모든 component마다 이렇게 작성할 수는 없음
좋은방법이 있을까?

####################################################################################################

#5 Error Boundaries with Higher Order Components

# higher-order component(HOC)
: HOC를 통해 모든 component를 보호할 수 있음
const BoundaryHOC = ProtectedComponent => class Boundary extends Component {
  state = {
    hasError: false
  }
  componentDidCatch = () => {
    this.setState({
      hasError: true
    })
  }
  render() {
    const { hasError } = this.state
    if (hasError) {
      return <ErrorFallback />
    } else {
      return <ProtectedComponent />
    }
  }
}

...

const PErrorMaker = BoundaryHOC(ErrorMaker)

...

const PPortals = BoundaryHOC(Portals)

# export default BoundaryHOC(App)
: application을 보호받고 싶을 때

####################################################################################################

#6 this.setState(null)

# this.setState(null)
: setState를 하면 component는 update하게 됨
이 기능은 언제 component를 update할지 안할지 결정할 수 있게 해줌

# return null
: setstate에 null을 대입하게 되면 state와 component를 더이상 update
const eatPizza = (state, props) => {
  const { pizzas } = state
  if (pizzas < MAX_PIZZAS) {
    return {
      pizzas: pizzas + 1
    }
  } else {
    return null
  }
}

####################################################################################################





