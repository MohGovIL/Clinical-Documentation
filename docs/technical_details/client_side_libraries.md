## [Redux](https://redux.js.org/) 
Redux is a powerful tool to manage state, “store”, on the global level of the  application, all the global data, “shared data”,  will be stored using Redux to make it easier for components to gain access to the data that they need without passing them on with “props” or  “HOC”(Higher order component).

Every piece of data that shared between to non-close component must be stored in redux. 

Redux has a lot of debugging utilities which helps speed up the developers job while debugging, it also helps with dividing the logical aspect of the project because each data has it’s own reducer and actions that are related to it, and it is also makes it easier to divide the work between the developers.

## [Material UI](https://material-ui.com/)
The design of the application based on google material UI, therefore we will have to implement it in every component it possible.

The responsive UI will be done with the material UI component as possible.

## [Styled-components](https://styled-components.com/)
The overwriting of the material ui style and another css setting will be done with styled-component.  

Every component has style.js file with css styling.

For example:
```
DefaultLogo\index.js


import React from 'react';
import DefaultStyledLogo from './Style';

const DefaultLogo = () => {
    return (
        <DefaultStyledLogo/>
    );
};

export default DefaultLogo;
```

DefaultLogo\Style.js
```
import styled from "styled-components";

export default styled.div`
  position: relative;
  width: 47px;
  height: 47px;
  background-color: #28d957;
  clip-path: circle(50% at 50% 50%);
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2);
  ::before{
    background-blend-mode: multiply;
    content: '';
    width: 47px;
    height: 47px;
    position: absolute;
    left: 50%;
    background-image: linear-gradient(to bottom, #0071ff, #0071ff);
    clip-path: circle(50% at 50% 50%);
  }
`;
```

## Translation - [i18next](https://react.i18next.com/)
All the data of the translation come from the existing mechanism of the Openemr (That we have expanded for our needs).

The constants and translations load from API using i18-next with ‘backend' plugin. The way to embed it in the components is according the react-i18-next documentation.
