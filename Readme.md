# **REACT ROUTER: UNDERSTANDING USEPARAMS HOOK**.
React router offers a powerful hook that helps in building React applications with multiple paths. This is known as the useParams hook. The purpose of this tutorial is to explain the meaning of useParams hook, benefits of useParams hook and steps in creating a react application that requires using useParams hook.
### **Prerequisite**:
It's important to have basic knowledge on React routing and JavaScript tools such as Arrays, Objects, Map function, and Destructuring. If you are unfamiliar with the above terms, we recommend you taking some time to learn and acquaint yourself before proceeding to get the best from this tutorial.
## **What is useParams Hook?**
The useParams hook is a React router hook that enables navigating and dynamic render of contents with multiple paths. Ecommerce and Blog apps are example of React applications with multiple paths that require implementing useParams hook. For instance, a blog app contains many blogs with a unique id, which will be used to retrieve and render blog details.
## **Benefit of useParams Hook**
* **Fewer codes:** The useParams hook aligns with the **Don't Repeat Yourself (DRY)** principle of programming. With useParams hook, we don't have to write codes repeatedly but rather retrieve and render contents based on its parameters.
* **Quick production:** Using hooks and tools such as useParams hook to write fewer codes help us finish projects quickly which in turn saves time and energy.
* **Codes reusability:** The useParams hook enable reusability of codes as for multiple parameters which reduces time and resources in developing software.
* **Accuracy:** The useParams hook retrieve and render contents of its parameters correctly without any mistakes.
* **Clean codes:** The useParams hook makes your codes understandable and maintainable.
## **Steps in applying useParams hook in React applications.**
In this section, we shall be building a simple ecommerce page that display products, whereby each product details will be retrieve and render. Let’s get started.
### **Assumption**
This section will assume that you have setup your react app with necessary routings. If you have not, check out this [**Link**](https://medium.com/@nehemiahdauda60/routing-in-react-applications-96340f2b07d5.) to setup your React application including installing React-router-dom. Also to note, the above link will serve as reference as we start building this app.

Firstly, lets creates an image folder in src directory. Insert all necessary images needed for the project.
* Creates route in App.js file for our pages.
```
<Routes>

    <Route path='/product/:id' element={<StoreDetails />}></Route>

</Routes>
```
The created route path has a placeholder as **id** in front colon. What the placeholder does is that react router will dynamically match the route to a url that matches /product/:id pattern in its path. For instance, if a url path takes in an id of 1, the url path will be product/1.
* Next Creates Product.js file in components folder, containing products information in an array. Each product should have a unique Id that  represents our parameters. Codes below
```
const Products = [
    {
        id: 1,
        title: "Products Name",
        description: "Product description",
        image:  require('../images/product-1.png')
    },
    {
        id: 2,
        title: "Products Name",
        description: "Product description",
        image:  require('../images/product-2.png')
    },
    {
        id: 9,
        description: "Product description",
        image: require('../images/product-3.png')
    }
]

export default Products;
```
* Next, creates a Card.js component, iterates through products in Product.js file using map function and render all products.
```
import { Link } from "react-router-dom";
import Products from "./Products";

const Card = () => {


    const arrayDataItems = Products.map(store =>{
        const {id, title, description, image} = store;
        return(
            <div key={ id } className="card">
                <img src={image} alt=""></img>
                <h3>{title}</h3>
                <p>{description.slice(0, 100)} <Link to={`/product/${id}`}>see more</Link></p>
            </div>
        )
    })

    return (
        <>
            <section className="card-section">
                {arrayDataItems}
            </section>
        </>
    );
};

export default Card;
```
In the above codes, map function was used to iterates through products which was imported from Products.js file. We also destruture our products object and save it to store. Note also we have a Link element that points to a url using backtick ( **`** ) and template literals ( **${}** ).
* In Home.js file in pages folder, import and render Card.js as seen in the codes below. (reference from [**React routing tutorial**](/https://medium.com/@nehemiahdauda60/routing-in-react-applications-96340f2b07d5.) )
```
import Card from "../components/Card"

const Home = () => {

    return (
        <>
            <h1>Home Page</h1>
            <Card />

        </>
    )
}

export default Home;
```
* Creates ProductDetails.js file in pages folder, import and implement useParams hook from react-router-dom.
```
import { useParams } from "react-router-dom";
import Products from "../components/Products";

const ProductDetails = () => {
    let { id } = useParams();
    const productDetails = Products.find(productDetails => String(productDetails.id) === id);

    return (
        <>
            <section key={id} className="details-section">
                <img src={productDetails.image} alt=""></img>
                <div>
                    <h3>{productDetails.title}</h3>
                    <p>{productDetails.description}</p>
                </div>
            </section>
       </>
    )
}

export default ProductDetails;
```
We firstly destructure our id and assign it to useParams function. Next, the find method assign to productDetails is use to match the id to and retrieve its content, which can further be render.
* Style your components in index.css file. I gave mine some little styling.
```
.card-section{
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  margin: 40px;
}

.card{
  padding: 1.2rem;
  border: 1px solid rgb(104, 101, 101);
}

.details-section{
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 30px;
  margin: 90px;
}
```
* Run server and see outcome.

In conclusion, this document provides a comprehensive knowledge on useParams hook. We looked at the benefits of useParams hook and also the process in applying useParams hook in react applications. Hope this was useful? Why not get started and perfect your skill in React.