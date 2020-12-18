# telaLogin
import React, {useEffect, useState} from 'react';
import {View, KeyboardAvoidingView, Image, TextInput, TouchableOpacity, Text, StyleSheet, Animated } from 'react-native';

export default function App() {

  const [offset] = useState(new Animated.ValueXY({x: 0, y:80}))
  const [opacity] =useState(new Animated.Value(0));

  useEffect(()=>{

    Animated.parallel([
      Animated.spring(offset.y, {
        toValue:0,
        speed:4,
        bounciness:20,
        //configuração necessario para usar o expo 
        useNativeDriver: true,
      }),
      Animated.timing(opacity, {
        toValue:1 ,
        duration:2000, 
        useNativeDriver: true,
      })
    ]).start();
    

  }, []);

  return (
    <KeyboardAvoidingView style={styles.background}>
      <View style={styles.conteinerLogo}>
        <Image
        source={require('./src/assets/logo.png')}
        />
      </View>

      <Animated.View 
        style={[
          styles.container,
          {
            opacity:opacity,
            transform:[{
              translateY:offset.y
            }]
          }
        ]}>
       <TextInput style={styles.input}
       placeholder="Email"
       autoCorrect={false}
       onChangeText={()=>{}}
       />

       <TextInput style={styles.input}
       placeholder="senha"
       autoCorrect={false}
       onChangeText={()=>{}}
       />

       <TouchableOpacity style={styles.btnSubmit}>
         <Text style={styles.submitText}>Acessar</Text>
       </TouchableOpacity>

       <TouchableOpacity style={styles.btnRegister}>
         <Text style={styles.registerText}>Criar Conta gratuita</Text>
       </TouchableOpacity>

      </Animated.View>
    </KeyboardAvoidingView>
  );
}

const styles = StyleSheet.create({
background: {
  flex:1,
  alignItems: 'center',
  justifyContent: 'center',
  backgroundColor: '#191919'
},
conteinerLogo:{
  flex:1,
  justifyContent:'center',
},
container:{
  flex:1,
  alignItems:'center',
  justifyContent:'center',
  width:'90%',
  paddingBottom:40
},
input:{
  backgroundColor: '#fff',
  width: '90%',
  marginBottom:15,
  color:'#222',
  fontSize:20,
  borderRadius:8,
  padding:8
},
btnSubmit:{
  color:'#35AAFF',
  width: '90%',
  height: 40,
  alignItems: 'center',
  justifyContent:'center',
  marginBottom: 10,
  backgroundColor: '#3CB389',
  borderRadius: 10
},
btnRegister:{
marginTop:10
},
submitText:{
  color:'white',
  fontSize:18
},
registerText:{
  color:'white',


}

})

