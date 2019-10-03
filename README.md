# React-Native-Flatlist-Refreshing
React Native Flatlist Refreshing

```
import React from "react"
import { 
  View, 
  ActivityIndicator,
  TextInput, 
  FlatList,
  YellowBox,
  StyleSheet,
  Image,
  Alert,
  Platform,
  TouchableOpacity,
  RefreshControl
} from 'react-native'

import { 
  Container,
  Content, 
  Card, 
  CardItem, 
  Body, 
  Text } from 'native-base';

import axios from 'axios';
import Header from './Header'

import ActionButton from 'react-native-action-button';
import Icon from 'react-native-vector-icons/Ionicons';

export const Addbtn = require('../../assets/add.png')


class TampilkanData extends React.Component {
  
 constructor(props) {
    super(props)
    this.state = {
        data: [],
        isOpen: false,
        isLoading: true, //refreshing
        refreshing: false //refreshing
    };
  }

//refreshing
FlatListItemSeparator = () => {
   return (
     <View
       style={{
         height: .5,
         width: "100%",
         backgroundColor: "#000",
       }}
     />
   );
 } //end refreshing

getdata = ()=>{
      return fetch('https://mpdyogyakarta.000webhostapp.com/api/Admin/list_kegiatan.php')
         .then((response) => response.text())
         .then((text) => text.length ? JSON.parse(text) : {})
         .then((text) => {
           this.setState({
             isLoading: false,
             data: text
           }, function() {
             // In this block you can do something with new state.
           });
         })
         .catch((error) => {
           console.error(error);
         });
}

componentDidMount() {
   this.getdata();
  }

//refreshing
_onRefresh(){
  this.setState({refreshing: true}) ;
   this.getdata().then(() => {
     this.setState({
       refreshing: false
     })
   })
}
//end refreshing

  AmbildataCuy=(id,judul_kegiatan, tanggal_kegiatan, lokasi_kegiatan, anggota_1, anggota_2, anggota_3, anggota_4, anggota_5, anggota_6, anggota_7, anggota_8, anggota_9, anggota_10)=>{
 
          this.props.navigation.navigate('DetailKegiatan', { 
 
            ID : id,
            JUDUL_KEGIATAN : judul_kegiatan,
            TANGGAL_KEGIATAN : tanggal_kegiatan,
            LOKASI_KEGIATAN : lokasi_kegiatan,
            ANGGOTA_1 : anggota_1,
            ANGGOTA_2 : anggota_2,
            ANGGOTA_3 : anggota_3,
            ANGGOTA_4 : anggota_4,
            ANGGOTA_5 : anggota_5,
            ANGGOTA_6 : anggota_6,
            ANGGOTA_7 : anggota_7,
            ANGGOTA_8 : anggota_8,
            ANGGOTA_9 : anggota_9,
            ANGGOTA_10 : anggota_10,
          });
     }



 renderItems = ({ item, index }) => {
       const {id,judul_kegiatan,tanggal_kegiatan,lokasi_kegiatan,anggota_1,anggota_2,anggota_3,anggota_4,anggota_5,anggota_6,anggota_7,anggota_8,anggota_9,anggota_10}=item
       return(
        <TouchableOpacity  onPress={this.AmbildataCuy.bind(
                        this, id,
                         judul_kegiatan,
                         tanggal_kegiatan, 
                         lokasi_kegiatan, 
                         anggota_1,
                         anggota_2,
                         anggota_3,
                         anggota_4,
                         anggota_5,
                         anggota_6,
                         anggota_7,
                         anggota_8,
                         anggota_9,
                         anggota_10,)} >
                          <Card>
                            <CardItem>
                              <Body>
                                  <Text>{judul_kegiatan}</Text>
                                  <Text>{tanggal_kegiatan}</Text>
                                  <Text>{lokasi_kegiatan}</Text>
                              </Body>
                            </CardItem>
                          </Card>
            </TouchableOpacity>
       )
    }
   

   render() {
    YellowBox.ignoreWarnings(['Encountered','ReferenceError']);
       return (
           <View style={{flex:1}}>
            <Header titleHeader='Masjid Pogung Dalangan'/>
                <FlatList
                   data={this.state.data}
                    ItemSeparatorComponent = {this.FlatListItemSeparator}
                   keyExtractor={item => item.toString()}
                   renderItem={this.renderItems}
                      
                      //refreshing
                     refreshControl={
                      <RefreshControl refreshing = {this.state.refreshing}
                        onRefresh  = {this._onRefresh.bind(this)}
                        />
                    } //end refreshing
                   />
                
                <ActionButton buttonColor="rgba(231,76,60,1)">
                    <ActionButton.Item buttonColor='#9b59b6' title="User Anggota" onPress={() => this.props.navigation.navigate('Adduser')}>
                      <Icon name="md-add-circle" style={styles.actionButtonIcon} />
                    </ActionButton.Item>
                    <ActionButton.Item buttonColor='#3498db' title="Kegiatan" onPress={() => this.props.navigation.navigate('Tambahdata')}>
                      <Icon name="md-add-circle" style={styles.actionButtonIcon} />
                    </ActionButton.Item>
              </ActionButton>
           </View>
        )
     }
  }


const styles = StyleSheet.create({

  TouchableOpacityStyle: {
    position: 'absolute',
    width: 50,
    height: 50,
    alignItems: 'center',
    justifyContent: 'center',
    right: 30,
    bottom: 30,
  },

  FloatingButtonStyle: {
    resizeMode: 'contain',
    width: 50,
    height: 50,
    //backgroundColor:'black'
  },

  actionButtonIcon: {
    fontSize: 20,
    height: 22,
    color: 'white',
  },
});
export default TampilkanData
```
