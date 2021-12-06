# [React Context API  and UserReducer  with Project](https://react-context-and-usereducer-project.netlify.app/)

![Imag  not found ](./preview.png)

> এই প্রজেক্ট  মাধ্যমে  রিএক্ট কনটেক্সট এর   মুটামুটি বেসিক ধারণা লাভ করা যাবে। 

> রিএক্ট কনটেক্সট হুক  ও  UserReducer  এর মাধ্যমে    ডাটা গুলো যে কোনো কম্পোনেন্ট গুলো  প্রপস ড্রিলিং ছাড়াই  এক্সেস করা  যায়. যার ফলে প্রজেক্ট এর   কোড গুলো অনেক কম হয় এবং ডাটা আদান প্রদান করতে অনেক সহজ হয়. উদাহরণ হিসেবে  একটা  ছবি নিচে দেওয়া হলো -   

### UserReducer Hook 
- এটা একটা রিএক্ট হুক  যেটা স্টেট ম্যানেজ করতে  ব্যবহার করা হয়।  
- কিন্তু আমরা জানি useState() হুক স্টেট ম্যানেজমেন্ট  করতে ব্যবহার হয়। 
- রিএক্ট  এ স্টেট চেঞ্জ  করার একটা মাকানিসম 

#### এখানে আমাদের কমন প্রশ্ন যে - 
> কেন আমরা   useReducer  ব্যবহার করবো ?

1. useState  হুক   বানানো হয়েছে  useReducer  এর উপর ব্যাস করে
1. useReducer () হুক userState  হুক এর এজটা বিকল্প 

#### তাহলে  useState   এবং useReducer   হুক এর  মাঝে পার্থক্য কি ? 

আমাদের রিএক্ট হুক  গুলোর মধ্যে আছে 
- useState
- useEffect 
- useMemo
- useRef
- useCallbakck 
- useContext
- useReducer etc. 

অর্থাৎ use    এর পরবর্তী শব্দের মাধ্যমে  আমরা সহজে  বুজতে  পারি যে সেটা  কোন বিষয়ের জন্য ব্যবহার করা হবে।  

#### তাহলে এখন আমাদের সবার কমন ,  প্রশ্ন তা হলো Reduce  কি ? 
> Reduce  রিএক্ট এর কোনো কনসেপ্ট না।  এটি জাভাস্ক্রিপ্ট এর কনসেপ্ট।  আমাদের প্রথমে বুজতে হবে জাভাস্ক্রিপ্ট এর reduce বিষয়টা কি ? 
> reduce শব্দের অর্থ ছোট করে নিয়ে আ।  array এর ভিতরে একাধিক এলিমেন্ট থাকে।  আর array এর একাধিক ভালুকে একটি ভ্যালু তে রূপান্তর   করার   কাজটা Array .Reduce   করে।  
> Reduce ফাঙ্কশন এ দুটি প্যারামিটার থাকে।  একটি accumulator  এবং অন্যটি currentValue . 
> accumulator  হলো আগের স্টেপ এর  রেজাল্ট। 
currentValue  হলো  Array তে  যখন Array .reduce ফাঙ্কশন কাজ করবে তখন যে  Array এলিমেন্ট নিয়ে কাজ করবে সেটা হলো currentValue . 
Reduce ফাঙ্কশন এ accumulator এ ডিফল্ট  মান ০ থাকে।  কিন্তু reduce এ Accumulator এর ম্যান নির্দিষ্ট করে দেওয়া  যায়।   যেটা পরবর্তীতে ডিফল্ট ম্যান হিসেবে কাজ করে 

### reduce  ও  useReducer  এর পার্থক্য 
![image ](./reduce.png)


### রিএক্ট এ useReducer ব্যবহার জিরার কনসেপ্ট হলো - 
- শুরুতে আমাদের  কে useReducer হুক ইম্পোর্ট করে নিতে হবে।  
- পরবর্তীতে আমাদের useReducer  এ দুটি  পেরামিটার (reducer, initializeState) হিসেবে ভ্যালু থাকে তা দিতে  হবে।
- কম্পোনেন্ট ফাঙ্কশন এর  উর্পরে অর্থাৎ বয়লার প্লেট  এ  initializeState   এবং reduce  ফাঙ্কশন দিতে হবে।  
- initializeState  এ ডিফল্ট হিসেবে নির্দিষ্ট ম্যান দিতে হবে।  
- reduce এ দুটি পেরামিটার (state , action )   থাকে। 
- অ্যাকশন বা  ইভেন্ট যখন কোনো ইভেন্ট ঘটে তখন আমাদের reduce এর action এ যখন  কোনো ইভেন্ট ঘটে তখন reducer এর স্টেট  পরিবর্তন হয়।  
- Reduce ফাঙ্কশন  এ Switch  ব্যবহার করে Action  দিতে   হয়  
- userReducer একটি Tuple  রিটার্ন করে।  
- Tuple  এ   প্রথমে আমরা State  এর value   পাই এবং দ্বিতীয় তে স্টেট Action  করার জন্য Dispatch  পেয়ে থাকি।  
#### Code  useReducer Hook use  simple  project 



```javascript 
import { useReducer } from 'react';

const initialState = 5;
const reducer = (state, action) => {
    switch (action) {
        case 'increment':
            return state + 1;
        case 'decrement':
            return state - 1;
        default:
            return state;
    }
};

export default function Counter() {
    const [count, dispatch] = useReducer(reducer, initialState);
    return (
        <div>
            <div>Count - {count}</div>
            <button type="button" onClick={() => dispatch('increment')}>
                Increment
            </button>
            <button type="button" onClick={() => dispatch('decrement')}>
                Decrement
            </button>
        </div>
    );
}
```



