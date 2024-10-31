import React, { useState, useRef, useEffect } from "react";
import {
    View,
    Text,
    TouchableOpacity,
    StyleSheet,
    Animated
} from "react-native";

interface SubTabMenuProps {
    menuOptions: string[];
    handleOptionPress: (option: string) => void;
    initialActiveTab?: string;
}

export default function SubTabMenu({ menuOptions, handleOptionPress, initialActiveTab }: SubTabMenuProps) {
    const [activeTab, setActiveTab] = useState(initialActiveTab || menuOptions[0]);
    const [tabWidths, setTabWidths] = useState<{ [key: string]: number }>({});
    const animatedValue = useRef(new Animated.Value(0)).current;

    useEffect(() => {
        const index = menuOptions.indexOf(activeTab);
        Animated.spring(animatedValue, {
            toValue: index,
            useNativeDriver: true,
            bounciness: 0,
        }).start();
    }, [activeTab]);

    const handlePress = (option: string) => {
        setActiveTab(option);
        handleOptionPress(option);
    };

    const indicatorPosition = animatedValue.interpolate({
        inputRange: menuOptions.map((_, i) => i),
        outputRange: menuOptions.map((option) => {
            const previousTabsWidth = menuOptions
                .slice(0, menuOptions.indexOf(option))
                .reduce((sum, tab) => sum + (tabWidths[tab] || 0), 0);
            return previousTabsWidth;
        }),
    });

    return (
        <View style={styles.container}>
            <Animated.View
                style={[
                    styles.indicator,
                    {
                        width: (tabWidths[activeTab] || 0) - 4,
                        transform: [{ translateX: indicatorPosition }],
                    },
                ]}
            />
            {menuOptions.map((option, index) => (
                <TouchableOpacity
                    key={index}
                    style={styles.menuOption}
                    onPress={() => handlePress(option)}
                    onLayout={(event) => {
                        const { width } = event.nativeEvent.layout;
                        setTabWidths((prev) => ({ ...prev, [option]: width }));
                    }}
                >
                    <Text style={[styles.menuText, activeTab === option && styles.activeText]}>
                        {option}
                    </Text>
                </TouchableOpacity>
            ))}
        </View>
    );
}

const styles = StyleSheet.create({
    container: {
        flexDirection: 'row',
        width: '98%',
        position: 'relative',
        alignItems: 'center',
        marginBottom: 10,
        backgroundColor: '#ade8f4',
        borderRadius: 10,
        padding: 2,
    },
    menuOption: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center',
        paddingVertical: 7,
    },
    menuText: {
        fontSize: 16,
        color: '#666',
    },
    activeText: {
        color: '#000',
        fontWeight: 'bold',
    },
    indicator: {
        position: 'absolute',
        height: '90%',
        backgroundColor: '#48cae4',
        borderRadius: 8,
        marginLeft: 4,
    },
});
