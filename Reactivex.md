## ReactiveX

Useful resource : https://www.learnrxjs.io

### Observables

Service.ts
```
    public get(id: number): Observable<Product> {
        return this.http.get<Unicorn>('http://example.com/api/product/' + id);
    }
```

Observables are triggered ONLY when subscribed
```
service.get(42).subscribe((product:Product) => { 
  // do something
  });
```

### Operators

Operators help to do some work on retreived object(s) before outputing it (like transforming, loggin, etc.)

```
service.getList()
  .pipe(
    flatMap(p => p), // convert array to a sequence of objects
    pluck('brandName'), // get one property from object
    map((brandName:string): string => slug(brandName)) // some transformation
  )
.subscribe((brandNameSluged:string) => { 
  // do something
  });
```

Other useful operators 
- from() : Turn an array, promise, or iterable into an observable
- of()
- reduce(accumulator:any, product:Product)
- mergeMap : useful for dependant asynchronous mapping (e.g : you get Product.categories array then call /categories/ID depending on the values)
- toArray()
- debounceTime(dueTime: number, scheduler: Scheduler): Observable : emits value once the dueTime has been reached. Useful for typeahead usecase
- forkJoin(...args, selector : function): Observable : When all observables complete, emit the last emitted value from each
