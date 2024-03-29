---
layout: layouts/blog.njk
---

[← Home](/)

# Windows 98 UI Project Experience

While doing the [Windows98 project](https://windows98-ui.netlify.app/), I've learned a lot, from technical stuff to the way I need to think to give the users a good experience.

## Understanding New Concepts of React

### Improved Way of Managing Children

One of the most interesting things that I learned doing this project was a new approach to managing the children of my React Components. It started with the `Tabs` component, which is the parent of the other three components: `TabList`, `Tab`, and `TabPanel`. Here's how it looks:

![Tabs component with a Windows 98 styling](/assets/blog/1/Screen%20Shot%202023-06-22%20at%202.44.31%20PM.png)

The challenge was that I had a variable called `currentTab` in `Tabs` that stored the selected tab value, and I needed all the children to access it. However, since I wanted the user to decide how many tabs they want, I didn't know how to pass `currentTab` without hardcoding how many tabs the `Tabs` component have.

Fortunately, I discovered a solution using React's `Children` and `isValidElement`. By mapping the `Children` and checking each child using `isValidElement` I was able to handle the children more effectively. `isValidElement` not only ensured that each child was a valid React element, but also simplified the management because the child elements were a `ReactNode`, and the `isValidElement` returned a `ReactElement`.

By having a `ReactElement`, now I was able to access the child's `key`, `props`, and `type`. This allowed me to return the `child.type` (since different types of children existed), assign the expected props based on each component's interface, and finally add the `currentTab` prop by default. This way, users had the flexibility to manage the number of tabs and navigate between them.

The code ended up looking like this:

```tsx
import {
  FunctionComponent,
  Children,
  PropsWithChildren,
  isValidElement,
  useState,
} from "react";
import "./styles.css";

interface Props extends PropsWithChildren {
  selectedTab?: number;
}

const Tabs: FunctionComponent<Props> = ({ children, selectedTab = 1 }) => {
  const [currentTab, setCurrentTab] = useState(selectedTab);

  const selectTab = function (value: number) {
    setCurrentTab(value);
  };
  const mappedChildren = Children.map(children, (child) => {
    if (isValidElement(child)) {
      return (
        <child.type
          {...child.props}
          onSelect={selectTab}
          selectedTab={currentTab}
        />
      );
    }
    return child;
  });

  return <div className="windowsTabs">{mappedChildren}</div>;
};

export default Tabs;
```

### Working with Icons

This project required me to learn how to manage icons. When I had the `Icons` folder with hundreds of images, I quickly realized that it would be impossible to make a component for each icon, so I did my research and discovered a straightforward approach using React.

To import an icon, all I needed to do was assign a name to the import and provide the directory:

```tsx
import MyIcon from "./components/icons/my-icon.png";
```

Then, I could simply use the assigned name as the `src` of an `img` tag:

```tsx
<img src={MyIcon} alt="example icon">
```

## Exploring CSS Tricks

To achieve the most accurate visual styles, I had to modify the default browser styling, particularly the scrollbar. This required me to learn about the WebKit extensions and understand how to utilize -webkit-scrollbar and its pseudo-classes. Initially, it seemed a bit confusing, but then I did some research and found [this CSS-tricks guide](https://css-tricks.com/custom-scrollbars-in-webkit/) that provided clear explanations and helped me grasp the concept.

In the end, I believe the custom scrollbar added a nice touch, and I learned something useful! Here's how it looks in action:

![Element with the windows98 scrollbar](/assets/blog/1/Screen%20Shot%202023-06-22%20at%204.05.57%20PM.png)

I also had to learn about `::before` to style the `TreeList` component, specifically the lines that connect the tree elements:

![TreeList windows98 component](/assets/blog/1/Screen%20Shot%202023-06-22%20at%204.13.09%20PM.png)

Overall, it was a useful and fun way to practice CSS techniques!

## Understanding npm and package.json

This is the first library that I create, so it required me to learn about npm and how to upload it. While figuring out npm, I also learned about managing the `package.json` file, particularly adding important details like the package name, version, and more.

Though not overly complicated, understanding these concepts was important.

## Prioritizing User Experience

Throughout this project, I had a realization that changed my perspective. It's no longer just about completing a cool project; now, I strive to create a great experience for the users.

When building a website, I aim to provide users with a smooth and intuitive navigation experience, regardless of the device they use. For libraries, my goal is to offer easy-to-use components that look appealing.

This shift in perspective occurred because I encountered challenges while using certain libraries. As a result, I focused on writing code that is easy to understand and use, even for someone new to it.

## Conclusion

It was a fun experience overall, all the blocks that I had were useful. I ended up learning a lot of different things. I will continue maintaining the library and adding new features, ensuring that my learning journey continues.
