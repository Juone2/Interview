### 설치하기

```bash
yarn add react-slick
yarn add -D slick-carousel # react-slick의 스타일 import 하기 위함
```

만약, **styled-components**와 함께 사용할 때는 다음과 같이 불러와야 합니다!

```
import 'slick-carousel/slick/slick.css';
import 'slick-carousel/slick/slick-theme.css';
```

### **Arrow 커스텀(스타일링)**

**NextArrow.tsx**

```tsx
interface NextArrowProps {
  className?: any;
  style?: any;
  onClick?: React.MouseEventHandler<HTMLDivElement>;
}

export default function NextArrow({ className, style, onClick }: NextArrowProps) {
  return <div className={className} style={{ ...style, display: 'block', background: 'red' }} onClick={onClick} />;
}
```

→ 이미지도 교체 가능

**CardSlider.tsx**

```tsx
import Slider from 'react-slick';

const CardSlier = () => {
	const settings = {
      dots: true,
      infinite: true,
      slidesToShow: 3,
      slidesToScroll: 1,
      nextArrow: <SampleNextArrow />,
      prevArrow: <SamplePrevArrow />};
	return(
		<Slider {...settings}>
		</Slider>);
};

export default CardSlider;
```

### dots 스타일링

**WaitingCardSlider.tsx**

```tsx
const Container = styled.div`
	width: 364px;
  height: 278px;
  .slick-dots {
    .slick-active {
      button::before {
        color: #c1c1c1;
      }
    }
    button::before {
      color: #e9e9e9;
    }
  }
`;
```

- `dot` 은 기본적으로 .slick-dots 클래스에 스타일링이 되어 있습니다.

### 최종코드

**WaitingCardSlider.tsx**

```tsx
export default function WaitingCardSlider() {
  const settings = {
    centerMode: true,
    dots: true,
    infinite: true,
    slidesToShow: 1,
    slidesToScroll: 1,
    arrows: false,
  };

  return (
    <Container>
      <Slider {...settings}>
				{/* WaitingCard는 그냥 예시일 뿐이므로, 서버에서 배너(이미지)를 배열로 담아주면, map으로 뿌리기 */}
        <WaitingCard
          thumbnail='https://dummyimage.com/364x278/000/fff'
          candy='https://dummyimage.com/70x70/000/fff'
          date={10}
          decs='캔디함에서 기다리고 있어요.'
          title='필보이드 핸드크림'
        />
        <WaitingCard
          thumbnail='https://dummyimage.com/364x278/000/fff'
          candy='https://dummyimage.com/70x70/000/fff'
          date={10}
          decs='캔디함에서 기다리고 있어요.'
          title='필보이드 핸드크림'
        />
        <WaitingCard
          thumbnail='https://dummyimage.com/364x278/000/fff'
          candy='https://dummyimage.com/70x70/000/fff'
          date={10}
          decs='캔디함에서 기다리고 있어요.'
          title='필보이드 핸드크림'
        />
        <WaitingCard
          thumbnail='https://dummyimage.com/364x278/000/fff'
          candy='https://dummyimage.com/70x70/000/fff'
          date={10}
          decs='캔디함에서 기다리고 있어요.'
          title='필보이드 핸드크림'
        />
      </Slider>
    </Container>
  );
}
```

- dots : 사진 밑에 뜨는 동그라미 적용 여부 (true/false)
- infinite : 슬라이드 반복 여부. true일 경우 마지막 슬라이드 다음이 다시 처음 슬라이드가 된다. (true/false)
- speed : 슬라이드 넘어가는 속도 (ms)
- slidesToShow : 한 번에 볼 수 있는 슬라이드의 개수
- slidesToScroll : 한 번에 넘어가는 슬라이드의 수
- arrows : 슬라이드 양 옆에 뜨는 화살표 표시 여부 (true/false)

### 공식문서

https://react-slick.neostack.com/docs/example/custom-arrows