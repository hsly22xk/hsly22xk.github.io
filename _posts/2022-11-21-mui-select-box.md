---
layout: single
title: "[Material UI/MUI] MUI Select Box 구현하기"
categories: MUI
tag: [기록, mui, material-ui]
author_profile: false
---

mui select box 구현하기.

## 개요

React에서 Select Box를 구현하려고 했을 때, select태그를 사용하는 방법도 있지만 mui를 활용하여 css도 깔끔하게 구현하는 방법을 사용해보았다.

## select태그를 사용하는 방법

먼저 select 태그를 활용하여 select box를 만든 예시이다.

```javascript
const fruit = ['grape', 'apple']

const A = () => {
 const [value, setValue] = useState('');

 ...

 const handleChange = (e) => {
   setValue(e.target.value);
 }
}

return (
  <>
  ...
    <select onChange={handleChange} value={value}>
      {fruit.map((el) => (
        <option value={el} key={el}>
          {el}
        </option>
      ))}
    </select>
   ...
  </>
)
```

useState로 상태변경함수를 하나 지정해준 후, 배열의 요소에 맞추어 onChange이벤트를 넣어준다.

배열의 요소들을 맵핑하여 요소들을 나타내준다.

select태그를 활용하여 select box를 만드는 가장 기본적인 방법이다.

## mui select 사용하기

[(공식문서)](https://mui.com/material-ui/react-select/)

하지만 나는 조금 더 깔끔해보이는 select box를 만들고 싶었다.

그래서 개발 중에 사용하고 있던 mui를 활용하여 select box를 만들어보기로 했다.

```javascript
// ① mui에서 필요한 요소들을 import해준다
// 만들고 싶은 상태의 요소들을 전부 import해준다
import { Select, MenuItem, FormControl } from '@mui/material';

const fruit = ['grape', 'apple']

const A = () => {
 const [value, setValue] = useState('');

 ...

 const handleChange = (e) => {
   const { value } = e.target;
   setValue(value);
 }
}

return (
  <>
    {/* FormControl의 사이즈는 알아서 조절해주면 됨 */}
    <FormControl required sx={{ m: 1, minWidth: 120 }}>
      {/* 나는 required label를 활용해주었다. 이 부분도 알아서 커스텀 할 수 있음 */}
      <Select
        labelId='demo-simple-select-required-label'
        id='demo-simple-select-required'
        value={selectedValue}
        label='Fruit *'
        onChange={handleChange}
      >
        <MenuItem value={fruit[0]}>grape</MenuItem>
        <MenuItem value={fruit[1]}>apple</MenuItem>
      </Select>
    </FormControl>
  </>
)
```

처음에는 mui의 Autocomplete를 사용해서 해보려했으나, 내가 원하는대로 구현이 되지 않았다.

그러던차에 select 태그가 생각났고, mui에도 똑같은 방법이 있지 않을까 하여 찾아보니 나왔다.
