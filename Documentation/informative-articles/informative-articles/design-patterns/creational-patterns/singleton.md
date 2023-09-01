# Singleton

A singleton is intended to provide only one instance of itself while facilitating a global point of access.

![singleton-2x.png](./attachments/singleton-2x.png)


```typescript 
class Singleton {
  private static instance: Singleton;

  private constructor() {}

  public static getInstance(): Singleton {
    if (!this.instance) {
      this.instance = new Singleton();
    }
    
    return this.instance;
  }
}

const instance = Singleton.getInstance();
const intance2 = Singleton.getIntstance();

console.log(instance === instance2); // true
```



Real-Life Example (Rick and Morty REST API with axios):

```typescript 
import Axios from "axios";

class APIClient {
  private static instance: APIClient;
  private static BASE_URL = "https://rickandmortyapi.com/api";
  public axiosClient: Axios;

  private constructor() {
    this.axiosClient = Axios.create({
      timeout: 15000,
      baseURL: this.BASE_URL,
    });
  }
  
  public static getInstance() {
    if (!this.instance) {
      this.instance = new APIClient();
    }
    
    return this.instance;
  }
}

export default APIClient.getInstance();
```


