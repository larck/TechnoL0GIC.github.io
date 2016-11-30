---
layout: post
title: "테스트 TEST 게시물 ARTICLE 테스트 TEST 게시물 ARTICLE"
description: "이것은 설명입니다. This is description"
date: 2016-11-30
tags: [test, web]
comments: true
share: true
---

지킬로 첫 포스팅 해보는데 하하하 재밌군
**정말** 재밌어 ***리얼리*** *꿀잼* 하

	굳굳
	
> 오오오

```javascript 
import React from 'react';
import Markdown from './Markdown';
import Profile from './Profile';
import Curriculum from './Curriculum';
import Tag from './Tag';
import Participants from './Participants';

class ApplyContainer extends React.Component {

  constructor(props) {
    super(props);

    //초기에 받아와서 제일 위의 커리큘럼 데이터를 밑에다 써줘

    this.state = {
      title: 'Title',
      tag: 'web',
      participants: 'Participants',
      markdown: '# Markdown',
      profileData: [
        {name: "개발하는데", desc: "주웅이 얼굴을 자꾸 보게되"}
      ],
      curriculumData: [
        {title: "최대한 많은양의 햄버거를 최단시간에 섭취할 수 있는 방법론", id:"1"},
        {title: "김동우의 연애사 전격공개", id:"2"},
        {title: "위 얼 오버워치", id:"3"}
      ]
    }
  }

  setContent(title, tag, participants, markdown, profileData) {
    this.setState({
      title,
      tag,
      participants,
      markdown,
      profileData
    }, ()=> {
      $("#marked").html(marked(this.state.markdown));
    });
  }

  setCurri() {
    //카테고리 필터링에 따라 받아오면 됨

    console.log($(".tag"));

    /* this.setState({
      curriculumData
    }); */
  }

  //카테고리 필터링은 누가하죠?..

  loadDetail(id) {

    //커리큘럼 클릭 이벤트임
    //id에 해당하는 데이터 불러와

    $.get( "index.html", function(data) {
      console.log(data);
    });

    if (id == 1) {
      this.setContent(
        '최대한 많은양의 햄버거를 최단시간에 섭취할 수 있는 방법론',
        'cs',
        '홍길동, 고길동, 정동윤',
        '# 엄마는 투사다',
        [
          {name: '이름', desc: '이 데스크가 책상 데스크는 아님'},
          {name: 'ㄹㅇ', desc: '디스크립션 약자지'},
          {name: '닥쳐', desc: 'ㄹㅇ 시끄러움'},
        ]
      );
    } else if (id == 2) {
      this.setContent(
        '김동우의 연애사 전격공개',
        'app',
        '김동우, 김동우2, 김동우3',
        '# 이거 렌더링 안댐asdfasdfafd ㅠ',
        [
          {name: '이름', desc: '이 데스ㅁㅁㄴㅇㅁㄴㅇㄹ크가 책상 데스크는 아님'},
          {name: 'ㄹㅇ', desc: '디스크립션 약자지'},
          {name: '닥쳐', desc: 'ㄹㅇ 시끄러움'},
        ]
      );
    } else if (id == 3) {
      this.setContent(
        '위얼 오버워치',
        'game',
        '루시우, 메르시, 아나, 라인하르트, 겐지',
        '# 시공의 폭풍',
        [
          {name: '루시우', desc: '춤 잘춤'},
          {name: '메르시', desc: '잘 날라댕김'},
          {name: '아나', desc: '아나;'},
          {name: '라인하르트', desc: '쿠팡맨'},
          {name: '겐지', desc: '?'}
        ]
      )
    }
  }

  render(){
    return (
      <div>
        <aside>
          <div className="category">
            <h5>카테고리</h5>
            <div className="tag" data-select="" data-tag="web" onClick={ ()=> this.setCurri() }><div className="square"></div>웹</div>
            <div className="tag" data-select="" data-tag="app" onClick={ ()=> this.setCurri() }><div className="square"></div>앱</div>
            <div className="tag" data-select="" data-tag="game" onClick={ ()=> this.setCurri() }><div className="square"></div>게임</div>
            <div className="tag" data-select="" data-tag="iot" onClick={ ()=> this.setCurri() }><div className="square"></div>사물인터넷</div>
            <div className="tag" data-select="" data-tag="program" onClick={ ()=> this.setCurri() }><div className="square"></div>프로그램</div>
            <div className="tag" data-select="" data-tag="cs" onClick={ ()=> this.setCurri() }><div className="square"></div>컴퓨터과학</div>
          </div>
          <div className="list">
            <h5>교육 커리큘럼</h5>
            {
              this.state.curriculumData.map((curriculum, i) => {
                return(
                  <Curriculum parent={ this } title={ curriculum.title } id={ curriculum.id } key={i}  />
                )
              })
            }
          </div>
        </aside>
        <div id="content">
          <div className="line-category"></div>
          <div className="box title">
            <div className="col">
              <h1> { this.state.title } </h1>
              <div className="info">
                <Tag category={ this.state.tag } />
                <Participants people={ this.state.participants } />
              </div>
            </div>
            <div className="col">
              <button className="fb"><img src="img/fb.svg" alt="페이스북으로 공유" /></button>
              <button className="tw"><img src="img/tw.svg" alt="트위터로 공유" /></button>
              <button className="kt"><img src="img/kt.svg" alt="카카오톡으로 공유" /></button>
            </div>
          </div>
          <div className="box content">
            <div id="marked" > </div>
            <textarea className="marked-temp" disabled>

            </textarea>
          </div>
          <div className="box sullivan">
            {
              this.state.profileData.map((profile, i) => {
                return(
                  <Profile name={profile.name} desc={profile.desc} key={i} />
                )
              })
            }
          </div>
        </div>
      </div>
    );
  }
}

export default ApplyContainer;

```