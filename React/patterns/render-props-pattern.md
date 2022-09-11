# Render Props Pattern | JavaScript Patterns

> ## Excerpt
> Website created for the FrontendMasters course on JavaScript Patterns by Lydia Hallie

---
Pass JSX elements to components through props

___

### [Overview](https://javascriptpatterns.vercel.app/patterns/react-patterns/conpres#overview)

With the Render Props pattern, we pass components as props to other components. The components that are passed as props can in turn receive props from that component.

Render props make it easy to reuse logic across multiple components.

___

### [Implementation](https://javascriptpatterns.vercel.app/patterns/react-patterns/conpres#implementation)

If we wanted to implement an `input` field with which a user can convert a temperature from Celsius to Kelvin and Fahrenheit, we can use the `renderKelvin` and `renderFahrenheit` render props.

These props receive the `value` of the input, which they convert to the correct temperature in either K or °F.

```
function Input(props) {
  const [value, setValue] = useState("");

  return (
    <>
      <input value={value} onChange={(e) => setValue(e.target.value)} />
      {props.renderKelvin({ value: value + 273.15 })}
      {props.renderFahrenheit({ value: (value * 9) / 5 + 32 })}
    </>
  );
}

export default function App() {
  return (
    <Input
      renderKelvin={({ value }) => <div className="temp">{value}K</div>}
      renderFahrenheit={({ value }) => <div className="temp">{value}°F</div>}
    />
  );
}
```

___

### [Tradeoffs](https://javascriptpatterns.vercel.app/patterns/react-patterns/conpres#tradeoffs)

**Reusability**: Since render props can be different each time, we can make components that receive render props highly reusable for multiple usecases.

**Separation of concerns**: We can separate our app's logic from rendering components through render props. The stateful component that receives a render prop can pass the data onto stateless components, which merely render the data.

**Solution to HOC problems**: Since we explicitly pass props, we solve the HOC's implicit props issue. The props that should get passed down to the element, are all visible in the render prop's arguments list. We know exactly where certain props come from.

**Unnecessary with Hooks**: Hooks changed the way we can add reusability and data sharing to components, which can replace the render props pattern in many cases.

___

### [Exercise](https://javascriptpatterns.vercel.app/patterns/react-patterns/conpres#exercise)

#### [Challenge](https://javascriptpatterns.vercel.app/patterns/react-patterns/conpres#challenge)

Refactor the following code so that `TemperatureConverter` uses the `renderKelvin` and `renderFahrenheit` props to render the `<Kelvin />` and `<Fahrenheit />` components.

#### [Solution](https://javascriptpatterns.vercel.app/patterns/react-patterns/conpres#solution)
