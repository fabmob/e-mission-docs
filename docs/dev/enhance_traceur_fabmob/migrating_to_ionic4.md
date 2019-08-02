# Migrating to Ionic 4
___

We are currently using the first version of Ionic which was launched in 2014 and stopped in 2017. Since that, Ionic deployed 3 versions. It was well known that Ionic 2 perfomances were better than its predecessor, so what about Ionic 1 perfomances compare to Ionic 4 perfomances ?

The main change of Ionic 4 is that it is now **framework-agnostic**, we can now use whatever we want, [**Ionic Components**](https://ionicframework.com/docs/components) do not depend of [**Angular**](https://angular.io/) anymore. Ionic 4 still integrates deeply Angular though. However, it is not the same Angular that we were used to. In fact, we were using [**AngularJS**](https://angularjs.org/), which is known as Angular 1.X. Since Angular 2, Angular is now a [TypeScript](https://www.typescriptlang.org/)-based front-end web applications framework. 

If we want to use Ionic 4, we may need to freeze the development of new functionnalities and start porting the current functionnalities in either Angular ([A Guide for Migrating to Ionic 4.0](https://ionicframework.com/blog/a-guide-for-migrating-to-ionic-4-0/)), [**Vue.JS**](https://vuejs.org/) or [**ReactJS**](https://reactjs.org/) which are supported by Ionic. However, Ionic is now working on [**Capacitor**](https://capacitor.ionicframework.com/) which can be seen as a substitute for [**Cordova**](https://cordova.apache.org/). If we are using React or Vue, [**Ionic CLI**](https://ionicframework.com/docs/cli) does not support **Cordova** integration for both frameworks so we may want to use Angular. 

## Angular or ReactJS or VueJS ?

As I said before, the main issue with Vue and React is that Ionic does not officially support Cordova with them. However, this mean that we will not be able to use the *ionic CLI tooling* such as `ionic serve`, `ionic deploy`, etc... But, we will be able to use the Cordova CLI which we are using right now. 

So, this is now just a story of preferences. Even if Vue is the framework which syntaxically looks more like **AngularJS**, the two other frameworks as their advantages and disadvantages. Nevertheless, as Ionic still integrates deeply Angular and that one of the big changes is that it is now fully using the capacities of Angular Router and the documentation is more thorough in Angular. 