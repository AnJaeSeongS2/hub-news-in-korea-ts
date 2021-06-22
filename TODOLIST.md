# TODOLIST

### 목표

* https://www.inflearn.com/course/quasar-%EA%B5%AC%EA%B8%80%EB%89%B4%EC%8A%A4 강의를 따라간다.
* 문제되는 부분은 알아서 해결한다.

| 색인 | 작업                                                         | 상태 | 달성률 | 예상 완료일 | 완료일 | 작업 소요시간 |
| ---- | ------------------------------------------------------------ | ---- | -----: | ----------: | -----: | ------------- |
| 1    | 4강 cors 대응책으로 cors proxy를 이용하는데, public url에서는 진행불가. 따라서 https://velog.io/@leejh3224/CORS-Real-examples-8yjnloovl5 참고 시작.<br />cors 는 https://cors-anywhere.herokuapp.com/ 을 통해 proxy처리. | DONE |   100% |       06-08 |  06-08 | 1h            |
| 2    | rss-parser 측에서 require('http') 부분에서 http를 resolve못하는 현상 제거<br />-> webpack v5 부터는 브라우저 호환성을 위했던 node.js 모듈에 대한 자동 polyfill을 제공하지 않는다. 결과적으로 bundle size를 줄였다. <br />-> ref: https://so-so.dev/tool/webpack/whats-different-in-webpack5/<br />-> ans1: 이전처럼 node 관련 polyfill을 전부 수행. node-polyfill-webpack-plugin<br /><br />-> ans2: http, https, timer등 필요부분만 추가. ex: module.exports.resolve.failback.http: require.resolve('http-browserify')<br />- webpack 공부 진행 | DONE |   100% |       06-10 |  06-20 | 1d            |
| 3    | typescript prj로 변경                                        | DONE |   100% |       06-23 |  06-23 | 30m           |
| 4    | colorhunt.co 에서 적절한 컬러배색 참고                       | DONE |   100% |       06-23 |  06-23 | 10m           |
| 5    | https://jsonplaceholder.typicode.com 을 이용해 api test call을 할 수 있다. | DONE |   100% |       06-23 |  06-23 | 10m           |

