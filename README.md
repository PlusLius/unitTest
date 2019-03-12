## 常见测试框架

- mocha 支持Node&Browser express.js
- jasmine支持Node&Browser Vue.js
- karma A Test-Runner 在不同的浏览- 器中跑测试用例 Angular
- jest React
零配置
内置代码覆盖率
内置Mocks

## Matchers

```
相等断言
toBe(value)： 比较数字、字符串
toEqual(value)： 比较对象、数组
toBeNull()
toBeUndefined()

包含断言
toHaveProperty(keyPath, value)： 是否有对应的属性
toContain(item)： 是否包含对应的值，括号里写上数组、字符串
toMatch(regexpOrString)： 括号里写上正则

逻辑断言,在JavaScript中，有六个falsy值：false，0，''，null， undefined，和NaN。其他一切都是Truthy。
toBeTruthy()
toBeFalsy()
oBeGreaterThan(number)： 大于
toBeLessThan(number)： 小于

not 取反
```

## Asyncchronous

```
//回调方式测试
test('the data is peanut butter', done => {
  function callback(data) {
    expect(data).toBe('peanut butter');
    done();
  }

  fetchData(callback);
});

//承诺验证
assertions（1）代表的是在当前的测试中至少有一个断言是被调用的，否则判定为失败
test('the data is peanut butter', () => {
  expect.assertions(1);
  return fetchData().then(data => {
    expect(data).toBe('peanut butter');
  });
});

//async await
test('the data is peanut butter', async () => {
  expect.assertions(1);
  const data = await fetchData();
  expect(data).toBe('peanut butter');
});

test('the fetch fails with an error', async () => {
  expect.assertions(1);
  try {
    await fetchData();
  } catch (e) {
    expect(e).toMatch('error');
  }
});
```

## mock

```
const mockCallback = jest.fn();
forEach([0, 1], mockCallback);

// 此模拟函数被调用了两次
expect(mockCallback.mock.calls.length).toBe(2);

// 第一次调用函数时的第一个参数是 0
expect(mockCallback.mock.calls[0][0]).toBe(0);

// 第二次调用函数时的第一个参数是 1
expect(mockCallback.mock.calls[1][0]).toBe(1);
```

## Global Hooks

```
//在运行测试套件的之前或之后执行
const globalDatabase = makeGlobalDatabase();

function cleanUpDatabase(db) {
  db.cleanUp();
}

afterAll(() => {
  cleanUpDatabase(globalDatabase);
});


const globalDatabase = makeGlobalDatabase();

function cleanUpDatabase(db) {
  db.cleanUp();
}

afterEach(() => {
  cleanUpDatabase(globalDatabase);
});

const globalDatabase = makeGlobalDatabase();

beforeAll(() => {
  // Clears the database and adds some testing data.
  // Jest will wait for this promise to resolve before running tests.
  return globalDatabase.clear().then(() => {
    return globalDatabase.insert({testData: 'foo'});
  });
});

const globalDatabase = makeGlobalDatabase();

beforeEach(() => {
  // Clears the database and adds some testing data.
  // Jest will wait for this promise to resolve before running tests.
  return globalDatabase.clear().then(() => {
    return globalDatabase.insert({testData: 'foo'});
  });
});
```

## describe

```
describe(name, fn)创建一个块，在一个“测试套件”中，将几个相关的测试组合在一起

  delicious: true,
  sour: false,
};

describe('my beverage', () => {
  test('is delicious', () => {
    expect(myBeverage.delicious).toBeTruthy();
  });

  test('is not sour', () => {
    expect(myBeverage.sour).toBeFalsy();
  });
});

```

## istanbul

```
File      |  % Stmts | % Branch |  % Funcs |  % Lines | Uncovered Line #s |
----------|----------|----------|----------|----------|-------------------|
All files |      100 |      100 |      100 |      100 |                   |
 dom.js   |      100 |      100 |      100 |      100 |                   |
 sum.js   |      100 |      100 |      100 |      100 |                   |
 tab.js   |      100 |      100 |      100 |      100 |                   |
----------|----------|----------|----------|----------|-------------------|

Line Coverage 是否每一行代码都被执行
Functions Coverage 是否每一个函数都被调用
Branch Coverage 是否每一个if/else分支都被执行
Statement Coverage 是否每一句代码都被执行
```

## Sinon辅助单元测试

```
业务代码发送网络请求，操作本地存储或者异步执行代码是用到，Sinon的功能就是在单元测试运行时替换这些复杂操作，简化单元测试环境

```

## Karma自动化单元测试

```
特点：
    1.可以在真实浏览器测试
    2.远程执行测试用例
    3.监控文件变化，自动执行测试
    4.可扩展
```

## enzyme

```
用来测试react组件

React提供两种渲染方式的单元测试
1.Shallow Rendering 虚拟dom,将组件渲染成虚拟dom,但只渲染一层,所以处理速度非常快
2.真实dom
```
