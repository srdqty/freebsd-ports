# Created by: Akinori MUSHA aka knu <knu@idaemons.org>
# $FreeBSD$

PORTNAME=	Log-Dispatch-Config
PORTVERSION=	1.04
PORTREVISION=	1
CATEGORIES=	devel sysutils perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	perl@FreeBSD.org
COMMENT=	Log4j equivalent for Perl

LICENSE=	ART10 GPLv1+
LICENSE_COMB=	dual

BUILD_DEPENDS=	p5-IO-stringy>=0:devel/p5-IO-stringy \
		p5-AppConfig>=1.52:devel/p5-AppConfig \
		p5-Log-Dispatch>=2:devel/p5-Log-Dispatch
RUN_DEPENDS:=	${BUILD_DEPENDS}

USES=		perl5
USE_PERL5=	configure
NO_ARCH=	yes

.include <bsd.port.mk>
