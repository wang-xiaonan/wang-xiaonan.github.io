---
layout: wiki
title: React 编码守则
categories: React
description: React 编码守则
keywords: react, 编码守则
---

> 守则自用，仅作参考

### 一、基础规则 

- 每个文件只包含一个React组件，文件名和组件名一致
- 使用JSX语法格式

### 二、命名

1. **拓展名**：统一使用jsx作为React组件拓展名

2. **文件名**：采用帕斯卡命名法，BasicTable.jsx

3. **组件命名**：使用文件名作为组件名，例如SiderCustom.jsx，组件名为SiderCustom。对于一个目录的根组件，应该使用 `index.jsx` 作为文件名，使用目录名作为组件名。

   ```
   -Header
     ├── Button.jsx
     ├── Logo.jspx
     └── index.jsx
     
   // 外部引用
   import Header from 'Header';
   ```


4. **引用命名**：组件引用采用帕斯卡命名法，HTML 标签、组件实例使用驼峰命名法

   ```react
   // 引用
   import React from 'react';
   import ModalForm from './ModalForm';
   // 实例
   const reservationCard = <ReservationCard />;
   ```

5. **文件夹名**：名称全部小写，尽量用贴近内容英文单词，单词间用`-`隔开

6. **属性命名**：属性命名使用驼峰命名法

   - 使用 `className` 代替 `class` 属性
   - 使用 `htmlFor` 代替 `for` 属性

7. **方法命名** ：


   - 事件处理函数：handleSomething 
   - 自定义事件属性名称：onSomething =  {this.handleSomething}

### 三、声明

1. **组件声明** ：采用以下格式声明组件

   ```react
   import React from 'react';

   class Page extends React.Component {
     render() {
       return (
         <div>
           {this.props.children}
         </div>
       )
     }
   }

   export default Page;
   // 或者
   import React,{ Component } from 'react';

   class Page extends Component {
     render() {
       return (
         <div>
           {this.props.children}
         </div>
       )
     }
   }

   export default Page;
   ```

### 四、空格
1. **自闭合标签** ：闭合标签前留有一个空格

   ```react
   <Foo />
   ```

2. **属性和子标签缩进** ：使用2个空格进行缩进

   ```react
   <App>
     <Hello />
   </App>
   ```

3. **标签属性** ：标签属性之间隔1个空格，属性名和`=`之间不能有空格

   ```react
   <BreadcrumbCustom first="form" second="basic form" />
   ```

4. **等号** ：方法函数`=`两边要有空格，标签属性`=`两边不能有空格

   ```react
   state = { visible: false }

   handleOk = (e) => {
     console.log(e);
     this.setState({
       visible: false,
     });
   }
   ```


### 五、对齐

1. **属性对齐方式**：参照 [Validate closing bracket location in JSX](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md)

   - 属性较少时可以行内排列(建议属性3个以内，且标签长度不超过80)
   - 属性较多时每行一个属性，闭合标签单独成行(属性超过3个，或者长度超过80)

   ```react
   // 较长时,分行显示时，标签后尖括号单独成行！
   <input  
     type="text"
     value={this.state.newDinosaurName}
     onChange={this.inputHandler.bind(this, 'newDinosaurName')}
   />

   // 短时
   <Foo bar="bar" baz="baz" />
   ```

### 六、引号和括号

1. 对于 `JSX` 使用双引号，对其它所有 JS 属性使用单引号

   > 为什么？因为 JSX 属性[不能包含被转移的引号](http://eslint.org/docs/rules/jsx-quotes)，并且双引号使得如 `"don't"` 一样的连接词很容易被输入。常规的 HTML 属性也应该使用双引号而不是单引号，JSX 属性反映了这个约定。

   ```react
   <Foo bar="bar" />
   <Foo style={{ left: '20px' }} />
   ```

2. **组件跨行** ：当组件跨行时，要用括号包裹 JSX 标签

  ```react
    // bad
    render() {
      return <MyComponent className="long body" foo="bar">
               <MyChild />
             </MyComponent>;
    }

    // good
    render() {
      return (
        <MyComponent className="long body" foo="bar">
          <MyChild />
        </MyComponent>
      );
    }

    // good, when single line
    render() {
      const body = <div>hello</div>;
      return <MyComponent>{body}</MyComponent>;
    }
  ```
### 七、注释

1. **组件头部信息注释** ：组件头部块级注释，内容包括：创建者、时间、组件信息

   (Atom package：File Header)
   ```react
   /**
    * @Author: wangxiaonan@xxx.com <wangxiaonan>
    * @Date:   2017-08-15 14:47
    * @Last modified by:   wangxiaonan
    * @Last modified time: 2017-08-15 15:28
    */
   import React from 'react';
   ```

2. **引入注释** ：组件引入注释使用`//`，注释和引入之间有1个空格

   ```react
   import React from 'react';
   // import ThemesCustom from './ThemesCustom'
   ```

3. **jsx注释** ：使用`{/* */}`注释

   ```react
   // 单行注释，不要换行
   {/*<ThemesCustom />*/}
   // 多行注释，收尾同行，不要单独一行
   {/*<Menu.Item key="full" onClick={this.screenFull} >
        <Icon type="arrows-alt" onClick={this.screenFull} />
       </Menu.Item>*/}
   ```

4. **方法注释** ：注释内容包括：方法描述、参数及含义、返回值

   ```react
   /**
    * Return the difference between the first array and
    * additional arrays.
    *
    * @param  {Array} `a`
    * @param  {Array} `b`
    * @return {Array}
    */
   ```

### 八、标签

1. 没有子组件的父组件使用自闭和标签
2. 如果组件有多行属性，闭合标签应写在新的一行上

### 九、方法顺序

1. 继承 react.Component 的类的方法遵循下面的顺序

   > 1. constructor
   > 2. optional static methods
   > 3. getChildContext
   > 4. componentWillMount
   > 5. componentDidMount
   > 6. componentWillReceiveProps
   > 7. shouldComponentUpdate
   > 8. componentWillUpdate
   > 9. componentDidUpdate
   > 10. componentWillUnmount
   > 11. clickHandlers or eventHandlers like onClickSubmit() or onChangeDescription()
   > 12. getter methods for render like getSelectReason() or getFooterContent()
   > 13. Optional render methods like renderNavigation() or renderProfilePicture()
   > 14. render



### 总结

### 参考

[JSX Style Guide](https://github.com/airbnb/javascript/tree/master/react) 

[eslint-plugin-react](https://github.com/yannickcr/eslint-plugin-react)