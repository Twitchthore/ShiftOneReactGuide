# ShiftOneReactGuide

*ShiftOne에서 사용하는 React and JSX Design GuideLine 입니다.*


## Table of Contents
1. [Basic Rules](#basic-rules)
1. [Naming](#naming)


## Basic Rules

 - 1파일에는 1개의 React Component를 포함하는 것을 원칙으로 함.
    - 그러나, 연관된 multiple[Staless, or Pure, Components]는 1개의 파일에 허용할수 있음. eslint: [`react/no-multi-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-multi-comp.md#ignorestateless).
 - JSX 파일 문법을 기본으로 하여 작성하도록 한다.
 - Type Script를 사용하여 작성하도록 한다.(향후 예정임)
 
 ## Naming
 
  - **확장자명** : .jsx 확장자로 작성하도록 한다. eslint: [`react/jsx-filename-extension`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-filename-extension.md).
  - **파일명**: 파스칼케이스(PascalCase)형식으로 작성하도록 한다. E.g., `ShiftOne.jsx`.
  - **레퍼런스명**: 리액트 컴포넌트는 파스칼케이스(PascalCase)로 작성하고, 그 레퍼런스는 카멜케이스(camelCase)로 작성하도록 한다. eslint: [`react/jsx-pascal-case`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-pascal-case.md)
  
    ```jsx
    // bad
    import shiftOne from './ShiftOne';
    
    //good
    import ShiftOne from './ShiftOne';
    
    //bad
    const ShiftOneItem = <ShiftOne/>;
    
    //good
    const shiftOneItem = <ShiftOne/>;
