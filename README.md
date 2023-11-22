# WeatherWardrobe-API ☀👚

This JSON API provides information about a collection of fashionable items across various categories. Each category contains a list of items with details such as ID, title, and an image URL.


## JSON File

The `api.json` file in this repository contains:
- Categories: The JSON file is an array of objects, each representing a specific category of fashion items.
- Category Object: Each category object has two properties:
  - "category": A string representing the category name (e.g., "Sweaters," "Tops," "Bottoms," "Accessories," "Shoes").
  - "items": An array containing objects representing individual fashion items within the category.
- Fashion Item Object: Each fashion item object has the following properties:
  - "id": An integer representing a unique identifier for the item.
  - "title": A string representing the title or name of the item.
  - "img": A string containing the URL to the image of the item.
<br>
 
  ```
  {
    "category": "Sweaters",
    "items": [
      {
        "id": 1,
        "title": "Weater Ribbed Sweater Mocha",
        "img": "//us.princesspolly.com/cdn/shop/files/0-modelinfo-dana-us2_7b02840f-2e7d-45de-8de0-5d235c923f2e_450x610.jpg?v=1693979671"
      },
      // Additonal items in the "Sweaters" category...
    ]
  }
```

### Accessing the JSON File

You can access the JSON file using the following URL:

- https://tishshaw.github.io/WeatherWardrobe-API/api.json

### Example Usage

Here's an example of how you can use the JSON file in your project:

```
// Import necessary React and React Native components
import React, { useState, useEffect } from 'react';
import { View, Text, FlatList, Image, StyleSheet } from 'react-native';

// Define the component
const ItemList = ({ category }) => {
  const [items, setItems] = useState([]);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch('https://tishshaw.github.io/WeatherWardrobe-API/api.json');
        const data = await response.json();
        const categoryData = data.find(item => item.category === category);

        if (categoryData) {
          setItems(categoryData.items);
        }
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    };

    fetchData();
  }, [category]);

  // Render each item in a FlatList
  const renderItem = ({ item }) => (
    <View style={styles.item}>
      <Text>ID: {item.id}</Text>
      <Text>Title: {item.title}</Text>
      <Image source={{ uri: item.img }} style={styles.image} />
    </View>
  );

  return (
    <View>
      <Text style={styles.heading}>{category}</Text>
      <FlatList
        data={items}
        renderItem={renderItem}
        keyExtractor={item => item.id.toString()}
      />
    </View>
  );
};

// Define styles using StyleSheet
const styles = StyleSheet.create({
  heading: {
    fontSize: 20,
    fontWeight: 'bold',
    marginBottom: 10,
  },
  item: {
    marginBottom: 20,
  },
  image: {
    width: 150,
    height: 150,
    resizeMode: 'cover',
  },
});

// Export the component
export default ItemList;

```


