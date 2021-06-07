## 프로젝트 목적
- Apollo, GrapthQL, React를 이용한 영화 웹 앱 만들기 
- server uri는 movieql 사용

## 설치
styled-components 설치
```shell
#npm 
npm install styled-components

#yarn
yarn add styled-components
```

Apollo-client / graphql 설치
```shell
#npm
npm install @apollo/client graphql

#yarn 
yarn add @apollo/client graphql
```

## Apollo-client 사용하기

- Apollo-client 초기화
```js
import React from "react";
import ReactDOM from "react-dom";
import App from "./components/App";
import { ApolloClient, 
         InMemoryCache,
         ApolloProvider,
         useQuery,
         gql
         } from "@apollo/client";
         

const client = new ApolloClient({
  uri: "http://....", // GraphQL 서버 URL
  cache: new InMemoryCache(),    // InMemoryCacheApollo Client가 쿼리 결과를 가져온 후 캐시하는 데 사용 하는의 인스턴스
  
  });
```  

- React에 연결
```js
ReactDOM.render(
  <ApolloProvider client={client}>
    <App />
  </ApolloProvider>,
  document.getElementById("root")
);

```

- 데이터 가져오기 - useQuery
 ```js
function ExchangeRates() {
  
  const { loading, error, data } = useQuery(gql`
    {
      rates(currency: "USD") {
        currency
        rate
      }
    }
  `);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error :(</p>;

  return data.rates.map(({ currency, rate }) => (
    <div key={currency}>
      <p>
        {currency}: {rate}
      </p>
    </div>
  ));
}

function App() {
  return (
    <div>
      <h2>My first Apollo app 🚀</h2>
      <ExchangeRates />
    </div>
  );
}
```


[출처] https://www.apollographql.com/docs/react/get-started/#3-connect-your-client-to-react

