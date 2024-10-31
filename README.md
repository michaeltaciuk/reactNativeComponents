# Some React Native Components

Sub Tab Menu
![Sub Tab Menu Demo](demoGifs/subTabMenu.gif)
Usage: 
<SubTabMenu
    menuOptions={['Checklist', 'About']}
    handleOptionPress={(option: string) => {
        tryHaptics('');
        setSubTab(option);
    }}
/>
