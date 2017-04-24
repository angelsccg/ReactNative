ģ��
����

��ES5����ʹ��CommonJS��׼������React������ͨ��require���У���������������

//ES5
var React = require("react");
var {
    Component,
    PropTypes
} = React;  //����React�������

var ReactNative = require("react-native");
var {
    Image,
    Text,
} = ReactNative;  //���þ����React Native���

��ES6�importд����Ϊ��׼

//ES6
import React, { 
    Component,
    PropTypes,
} from 'react';
import {
    Image,
    Text
} from 'react-native'

����������

��ES5�Ҫ����һ��������ģ���ã�һ��ͨ��module.exports������

//ES5
var MyComponent = React.createClass({
    ...
});
module.exports = MyComponent;

��ES6�ͨ����export default��ʵ����ͬ�Ĺ��ܣ�

//ES6
export default class MyComponent extends Component{
    ...
}

���õ�ʱ��Ҳ���ƣ�

//ES5
var MyComponent = require('./MyComponent');

//ES6
import MyComponent from './MyComponent';

ע�⵼��͵�����д���������ף����ܻ��ã�
�������

��ES5�ͨ��ͨ��React.createClass������һ������࣬��������

//ES5
var Photo = React.createClass({
    render: function() {
        return (
            <Image source={this.props.source} />
        );
    },
});

��ES6�����ͨ������һ���̳���React.Component��class������һ������࣬��������

//ES6
class Photo extends React.Component {
    render() {
        return (
            <Image source={this.props.source} />
        );
    }
}

��������巽��

���������������Կ�������������巽�������� ����: function()��д��������ֱ��������()���ڷ��������Ҳ�����ж����ˡ�

//ES5 
var Photo = React.createClass({
    componentWillMount: function(){

    },
    render: function() {
        return (
            <Image source={this.props.source} />
        );
    },
});

//ES6
class Photo extends React.Component {
    componentWillMount() {

    }
    render() {
        return (
            <Image source={this.props.source} />
        );
    }
}

����������������ͺ�Ĭ������

��ES5��������ͺ�Ĭ�����Էֱ�ͨ��propTypes��Ա��getDefaultProps������ʵ��

//ES5 
var Video = React.createClass({
    getDefaultProps: function() {
        return {
            autoPlay: false,
            maxLoops: 10,
        };
    },
    propTypes: {
        autoPlay: React.PropTypes.bool.isRequired,
        maxLoops: React.PropTypes.number.isRequired,
        posterFrameSrc: React.PropTypes.string.isRequired,
        videoSrc: React.PropTypes.string.isRequired,
    },
    render: function() {
        return (
            <View />
        );
    },
});

��ES6�����ͳһʹ��static��Ա��ʵ��

//ES6
class Video extends React.Component {
    static defaultProps = {
        autoPlay: false,
        maxLoops: 10,
    };  // ע�������зֺ�
    static propTypes = {
        autoPlay: React.PropTypes.bool.isRequired,
        maxLoops: React.PropTypes.number.isRequired,
        posterFrameSrc: React.PropTypes.string.isRequired,
        videoSrc: React.PropTypes.string.isRequired,
    };  // ע�������зֺ�
    render() {
        return (
            <View />
        );
    } // ע�������û�зֺ�Ҳû�ж���
}

Ҳ������ôд����Ȼ���Ƽ��������������ʱ����Ӧ��������������˼��

//ES6
class Video extends React.Component {
    render() {
        return (
            <View />
        );
    }
}
Video.defaultProps = {
    autoPlay: false,
    maxLoops: 10,
};
Video.propTypes = {
    autoPlay: React.PropTypes.bool.isRequired,
    maxLoops: React.PropTypes.number.isRequired,
    posterFrameSrc: React.PropTypes.string.isRequired,
    videoSrc: React.PropTypes.string.isRequired,
};

ע��: ��React�����߶��ԣ�static��Ա��IE10��֮ǰ�汾���ܱ��̳У�����IE11������������Ͽ��ԣ�����ʱ������һЩ���⡣React Native�����߿��Բ��õ���������⡣
��ʼ��state

ES5��������ƣ�

//ES5 
var Video = React.createClass({
    getInitialState: function() {
        return {
            loopsRemaining: this.props.maxLoops,
        };
    },
})

ES6�£�������д����

//ES6
class Video extends React.Component {
    state = {
        loopsRemaining: this.props.maxLoops,
    }
}

���������Ƽ����������ڹ��캯���г�ʼ���������㻹���Ը�����Ҫ��һЩ���㣩��

//ES6
class Video extends React.Component {
    constructor(props){
        super(props);
        this.state = {
            loopsRemaining: this.props.maxLoops,
        };
    }
}

�ѷ�����Ϊ�ص��ṩ

�ܶ�ϰ����ES6���û������������ES5�¿�����ô����

//ES5
var PostInfo = React.createClass({
    handleOptionsButtonClick: function(e) {
        // Here, 'this' refers to the component instance.
        this.setState({showOptionsModal: true});
    },
    render: function(){
        return (
            <TouchableHighlight onPress={this.handleOptionsButtonClick}>
                <Text>{this.props.label}</Text>
            </TouchableHighlight>
        )
    },
});

��ES5�£�React.createClass������еķ�����bindһ�飬���������ύ������ĵط���Ϊ�ص���������this����仯�����ٷ���������Ϊ�ⷴ���ǲ���׼���������ġ�

��ES6�£�����Ҫͨ��bind����this���ã�����ʹ�ü�ͷ����������󶨵�ǰscope��this���ã�������

//ES6
class PostInfo extends React.Component
{
    handleOptionsButtonClick(e){
        this.setState({showOptionsModal: true});
    }
    render(){
        return (
            <TouchableHighlight 
                onPress={this.handleOptionsButtonClick.bind(this)}
                onPress={e=>this.handleOptionsButtonClick(e)}
                >
                <Text>{this.props.label}</Text>
            </TouchableHighlight>
        )
    },
}

��ͷ����ʵ�����������ﶨ����һ����ʱ�ĺ�������ͷ�����ļ�ͷ=>֮ǰ��һ�������š������Ĳ�������������������Ķ��������������ͷ֮�������һ�����ʽ����Ϊ�����ķ���ֵ�����������û���������ĺ����壨��Ҫ����ͨ��return������ֵ�����򷵻ص���undefined����

// ��ͷ����������
()=>1
v=>v+1
(a,b)=>a+b
()=>{
    alert("foo");
}
e=>{
    if (e == 0){
        return 0;
    }
    return 1000/e;
}

��Ҫע����ǣ�������bind���Ǽ�ͷ������ÿ�α�ִ�ж����ص���һ���µĺ������ã��������㻹��Ҫ����������ȥ��һЩ������飨Ʃ��ж�ؼ�����������ô������Լ������������

// ���������
class PauseMenu extends React.Component{
    componentWillMount(){
        AppStateIOS.addEventListener('change', this.onAppPaused.bind(this));
    }
    componentDidUnmount(){
        AppStateIOS.removeEventListener('change', this.onAppPaused.bind(this));
    }
    onAppPaused(event){
    }
}

// ��ȷ������
class PauseMenu extends React.Component{
    constructor(props){
        super(props);
        this._onAppPaused = this.onAppPaused.bind(this);
    }
    componentWillMount(){
        AppStateIOS.addEventListener('change', this._onAppPaused);
    }
    componentDidUnmount(){
        AppStateIOS.removeEventListener('change', this._onAppPaused);
    }
    onAppPaused(event){
    }
}

��������������ǻ�ѧϰ��һ���µ�������

// ��ȷ������
class PauseMenu extends React.Component{
    componentWillMount(){
        AppStateIOS.addEventListener('change', this.onAppPaused);
    }
    componentDidUnmount(){
        AppStateIOS.removeEventListener('change', this.onAppPaused);
    }
    onAppPaused = (event) => {
        //�ѷ���ֱ����Ϊһ��arrow function�����������壬��ʼ����ʱ��Ͱ󶨺���thisָ��
    }
}

Mixins

��ES5�£����Ǿ���ʹ��mixin��Ϊ���ǵ������һЩ�µķ�����Ʃ��PureRenderMixin

var PureRenderMixin = require('react-addons-pure-render-mixin');
React.createClass({
  mixins: [PureRenderMixin],

  render: function() {
    return <div className={this.props.className}>foo</div>;
  }
});

Ȼ�����ڹٷ��Ѿ����ٴ�����ES6���������Mixin������˵��Mixins Are Dead. Long Live Composition��

�������Ҫ����ʹ��mixin��������һЩ�������ķ��������ã�Ʃ���������

�����ٷ��Ƽ������ڿ��д�߶��ԣ�Ӧ���������Mixin�ı�д��ʽ���������ᵽSebastian Markb?ge��һ�δ����Ƽ���һ���µı��뷽ʽ��

//Enhance.js
import { Component } from "React";

export var Enhance = ComposedComponent => class extends Component {
    constructor() {
        this.state = { data: null };
    }
    componentDidMount() {
        this.setState({ data: 'Hello' });
    }
    render() {
        return <ComposedComponent {...this.props} data={this.state.data} />;
    }
};

//HigherOrderComponent.js
import { Enhance } from "./Enhance";

class MyComponent {
    render() {
        if (!this.data) return <div>Waiting...</div>;
        return <div>{this.data}</div>;
    }
}

export default Enhance(MyComponent); // Enhanced component

��һ������ǿ����������ĳ��������һЩ���������ҷ���һ�����࣬��������ʵ��mixin��ʵ�ֵĴ󲿷�����
ES6+�����������ô�
�⹹&������չ

���ʹ��ES6+�Ľ⹹��������չ�����Ǹ����Ӵ���һ�����Ը�Ϊ�����ˡ�������Ӱ�className������������Դ��ݸ�div��ǩ��

class AutoloadingPostsGrid extends React.Component {
    render() {
        var {
            className,
            ...others,  // contains all properties of this.props except for className
        } = this.props;
        return (
            <div className={className}>
                <PostsGrid {...others} />
                <button onClick={this.handleLoadMoreClick}>Load more</button>
            </div>
        );
    }
}

��������д�������Ǵ����������Ե�ͬʱ���ø����µ�classNameֵ��

<div {...this.props} className="override">
    ��
</div>

����������෴�����������û�а���className�����ṩĬ�ϵ�ֵ��������������Ѿ������ˣ���ʹ�������е�ֵ

<div className="base" {...this.props}>
    ��
</div>
