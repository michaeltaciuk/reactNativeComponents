# Some React Native Components

## Sub Tab Menu

This component displays a sub-menu with tabs that users can switch between, allowing for different content to be shown based on the selected tab.

### Demo
![Sub Tab Menu Demo](demoGifs/subTabMenu.gif)

### Usage
```jsx
<SubTabMenu
    menuOptions={['Checklist', 'About']}
    handleOptionPress={(option: string) => {
        tryHaptics('');
        setSubTab(option);
    }}
/>
