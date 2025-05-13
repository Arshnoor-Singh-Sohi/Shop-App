# Shop-App: Flutter E-Commerce Application


## 📑 Table of Contents

- [Introduction](#introduction)
- [Key Features](#key-features)
- [Technology Stack](#technology-stack)
- [Application Architecture](#application-architecture)
- [UI Components](#ui-components)
- [State Management](#state-management)
- [Project Structure](#project-structure)
- [Screens](#screens)
  - [Products Screen](#products-screen)
  - [Product Details Screen](#product-details-screen)
  - [Cart Screen](#cart-screen)
- [Data Flow](#data-flow)
- [Responsive Design](#responsive-design)
- [Installation Guide](#installation-guide)
- [Usage Guide](#usage-guide)
- [Performance Optimizations](#performance-optimizations)
- [Future Enhancements](#future-enhancements)

## Introduction

Shop-App is a sleek, modern e-commerce mobile application built with Flutter that offers a streamlined shopping experience for shoe enthusiasts. The application provides an intuitive interface for browsing products, viewing details, filtering by categories, selecting sizes, and managing a shopping cart, all with smooth animations and a responsive design that works across multiple device sizes.

The project demonstrates clean architecture principles, effective state management with Provider, and responsive UI design practices in Flutter, making it an excellent reference for mobile e-commerce implementations.

## Key Features

- **Intuitive Product Browsing**: Clean layout for easy product discovery
- **Category Filtering**: Filter products by brand (Nike, Adidas, Bata)
- **Detailed Product View**: View product images, prices, and available sizes
- **Size Selection**: Choose from available sizes before adding to cart
- **Shopping Cart Management**: Add/remove items and view cart contents
- **Responsive Design**: Adapts to different screen sizes (mobile, tablet)
- **Smooth Animations**: Polished transitions between screens and actions
- **Consistent Theming**: Custom color scheme and typography across the app
- **Visual Feedback**: User notifications for actions like adding to cart

## Technology Stack

<table>
  <tr>
    <th>Category</th>
    <th>Technology</th>
    <th>Purpose</th>
  </tr>
  <tr>
    <td>Framework</td>
    <td>Flutter</td>
    <td>Cross-platform UI development</td>
  </tr>
  <tr>
    <td>Language</td>
    <td>Dart</td>
    <td>Application logic and UI implementation</td>
  </tr>
  <tr>
    <td>State Management</td>
    <td>Provider</td>
    <td>Simplified state management across widgets</td>
  </tr>
  <tr>
    <td>Navigation</td>
    <td>Flutter Navigation</td>
    <td>Screen transitions and routing</td>
  </tr>
  <tr>
    <td>UI Components</td>
    <td>Material Design</td>
    <td>Consistent and responsive interface elements</td>
  </tr>
  <tr>
    <td>Assets</td>
    <td>Local Images</td>
    <td>Product images and icons</td>
  </tr>
  <tr>
    <td>Fonts</td>
    <td>Lato</td>
    <td>Custom typography throughout the app</td>
  </tr>
</table>

## Application Architecture

Shop-App follows a clean architecture pattern with separation of concerns:


1. **UI Layer**: Screen and widget components that users interact with
   - Screens (HomePage, ProductDetailsPage, CartPage)
   - Widgets (ProductCard, ProductList)

2. **State Management Layer**: Provider implementation for app state
   - CartProvider for shopping cart operations
   - ChangeNotifier pattern for UI updates

3. **Data Layer**: Product data and models
   - Static product data in global_variables.dart
   - Product and cart item data structures

The application architecture ensures:
- Clear separation between UI, business logic, and data
- Predictable state management
- Easily maintainable and testable code
- Efficient rebuilds with the Provider pattern

## UI Components

The app utilizes a custom theme with consistent styling throughout:

```dart
theme: ThemeData(
  fontFamily: 'Lato',
  colorScheme: ColorScheme.fromSeed(
    seedColor: const Color.fromRGBO(254, 206, 1, 1),
    primary: const Color.fromRGBO(254, 206, 1, 1),
  ),
  // Other theme configurations...
),
```

Key UI components include:

1. **ProductCard**: Displays product information in a visually appealing card format
2. **Product Filtering Chips**: Interactive filter options for browsing by category
3. **Size Selection**: Interactive size picker in the product details page
4. **Cart Item**: Individual cart item with image, title, and removal option
5. **Bottom Navigation**: Persistent navigation between home and cart screens

## State Management

Shop-App implements the Provider pattern for state management, offering a lightweight and efficient solution for sharing and updating state across the widget tree.

```dart
// CartProvider implementation
class CartProvider extends ChangeNotifier {
  final List<Map<String, dynamic>> cart = [];

  void addProduct(Map<String, dynamic> product) {
    cart.add(product);
    notifyListeners();
  }

  void removeProduct(Map<String, dynamic> product) {
    cart.remove(product);
    notifyListeners();
  }
}
```

The Provider implementation:
- Centralizes shopping cart state
- Provides simple methods for adding and removing products
- Triggers UI updates with notifyListeners() when the state changes
- Allows widgets to watch or read cart state as needed

Example of consuming the provider:
```dart
// Reading cart data
final cart = context.watch<CartProvider>().cart;

// Updating cart
context.read<CartProvider>().addProduct(product);
```

## Project Structure

The project follows a feature-based organization:

```
shop_app/
├── lib/
│   ├── main.dart              # Application entry point
│   ├── global_variables.dart  # Static product data
│   ├── pages/                 # Main screens
│   │   ├── home_page.dart     # Main container with navigation
│   │   ├── cart_page.dart     # Shopping cart screen
│   │   └── product_details_page.dart  # Product details view
│   ├── providers/             # State management
│   │   └── cart_provider.dart # Shopping cart state
│   └── widgets/               # Reusable UI components
│       ├── product_card.dart  # Product display card
│       └── product_list.dart  # Grid/list of products
├── assets/                    # Static resources
│   ├── images/                # Product images
│   └── fonts/                 # Custom typography
└── pubspec.yaml               # Project configuration
```

## Screens

### Products Screen

The Products Screen serves as the main entry point for users to browse the available products.


**Key Features:**
- Product grid/list with visually appealing cards
- Filter chips for product categories (All, Adidas, Nike, Bata)
- Search bar for product discovery
- Responsive layout that adapts to screen size (grid for larger screens, list for smaller ones)
- Alternating background colors for visual interest
- Custom header with app title

**Implementation Highlights:**
- Uses a `ListView.builder` or `GridView.builder` based on screen width
- Implements stateful widget for filter selection
- Integrates gesture detection for product selection

### Product Details Screen

The Product Details Screen provides comprehensive information about a selected product, allowing users to choose a size and add items to their cart.


**Key Features:**
- Large product image
- Product title and price
- Size selection with interactive chips
- Add to cart button with visual feedback
- Consistent styling with main app theme

**Implementation Highlights:**
- Maintains selected size in local state
- Validates size selection before cart addition
- Provides user feedback through SnackBar notifications
- Uses a bottom-aligned container for size and add-to-cart options

### Cart Screen

The Cart Screen displays all items added to the shopping cart and allows for item management.


**Key Features:**
- List of cart items with product image and details
- Delete functionality with confirmation dialog
- Clean, minimalist design for easy reading
- Consistent styling with main app theme

**Implementation Highlights:**
- Consumes cart state from CartProvider
- Implements AlertDialog for delete confirmation
- Uses ListTile for efficient list rendering

## Data Flow

1. **Product Data Source**: Static product data in global_variables.dart
2. **Product Selection Flow**:
   - User browses products in ProductList
   - User selects a product to view details
   - ProductDetailsPage receives the selected product data
   - User selects a size and adds to cart
   - CartProvider updates the cart state
3. **Cart Management Flow**:
   - CartPage displays products from CartProvider
   - User can remove items from the cart
   - CartProvider updates the state and notifies listeners
   - UI reflects the updated cart state

## Responsive Design

Shop-App implements a responsive design that adapts to different screen sizes:

```dart
// Example of responsive design implementation
Expanded(
  child: size.width > 650 
    ? GridView.builder(/* Grid layout for larger screens */) 
    : ListView.builder(/* List layout for smaller screens */),
)
```

Responsive features include:
- Flexible layouts that adapt to screen dimensions
- GridView for larger screens, ListView for smaller screens
- Appropriately sized text and UI elements
- Consistent spacing and padding across device sizes

## Installation Guide

### Prerequisites

- Flutter SDK 3.0.0 or higher
- Dart SDK 3.0.0 or higher
- Android Studio / VS Code with Flutter extension
- Android emulator or physical device (Android 5.0+)
- iOS simulator or physical device (iOS 11.0+)

### Installation Steps

1. Clone the repository:
   ```
   git clone https://github.com/Arshnoor-Singh-Sohi/Shop-App.git
   ```

2. Navigate to the project directory:
   ```
   cd Shop-App
   ```

3. Install dependencies:
   ```
   flutter pub get
   ```

4. Run the application:
   ```
   flutter run
   ```

## Usage Guide

### Browsing Products

1. Open the application
2. Browse the product list on the home screen
3. Use the category filters at the top to find specific brands
4. Tap on a product card to view its details

### Product Details and Cart

1. On the product details screen, select an available size
2. Tap "Add to Cart" to add the product to your shopping cart
3. A notification will confirm the addition
4. Navigate to the cart using the bottom navigation bar
5. View your cart items and remove unwanted products

## Performance Optimizations

Shop-App implements several performance optimizations:

1. **Efficient Widget Rebuilds**: Using Provider to rebuild only affected widgets
2. **IndexedStack**: Maintains the state of screens when switching between them
3. **ListView.builder/GridView.builder**: Creates views lazily as they scroll into view
4. **Const Constructors**: Optimizes widget creation where possible
5. **Image Asset Optimization**: Pre-sized images for better loading performance

## Future Enhancements

1. **Backend Integration**: Connect to a real API for dynamic product data
2. **User Authentication**: Add login/signup functionality
3. **Wishlist Feature**: Allow users to save products for later
4. **Product Reviews**: Enable users to view and add product reviews
5. **Payment Integration**: Add checkout and payment processing
6. **Order History**: Track past orders and their status
7. **Push Notifications**: Alert users about order updates and promotions
8. **Search Functionality**: Implement product search with filtering
9. **User Profiles**: Allow users to save preferences and addresses
10. **Dark Mode**: Add theme toggle for light/dark mode preferences

---

This project demonstrates Flutter's capabilities for building sophisticated e-commerce applications with clean architecture, effective state management, and responsive design principles.
